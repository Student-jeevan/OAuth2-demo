# Spring Boot OAuth2 Demo: SpringOAuth2Demo

This is a **Spring Boot demo application** showcasing **OAuth2 login integration** with **Google** and **GitHub**.  
Users can log in using their Google or GitHub accounts. The project uses **environment variables** to securely manage OAuth client credentials.

---

## 🛠️ Tech Stack & Configuration

| Technology              | Role / Purpose                        |
|-------------------------|--------------------------------------|
| Spring Boot             | Application Framework                 |
| Spring Security 6+      | Security / OAuth2 Integration         |
| OAuth2                  | Google & GitHub Login                 |
| Maven                   | Build / Dependency Management         |
| Lombok                  | Boilerplate Code Reduction            |
| MySQL (Optional)        | Persistent Storage (if used)         |

---

## 🌐 API Endpoints

**Base URL:** `http://localhost:8080`  

### Authentication & Public Endpoints (No OAuth2 Required)

| Method | URL     | Description          |
|--------|---------|--------------------|
| GET    | `/home` | Public welcome page |

> ⚠️ All other endpoints are secured. Users must log in via **Google** or **GitHub** OAuth2 to access them. Spring Security automatically handles the redirection to the OAuth2 provider.  

---

### Secured Resource Endpoints (OAuth2 Required)

To access these, users must be logged in via Google or GitHub OAuth2:

| Method | URL          | Description                          |
|--------|--------------|--------------------------------------|
| GET    | `/user`      | Returns authenticated user info      |
| Any    | Other routes | Secured by default, requires OAuth2  |

---

## 🌐 How to Configure OAuth2

### 1️⃣ Google OAuth2 Setup

1. Go to [Google Cloud Console → APIs & Services → Credentials](https://console.cloud.google.com/apis/credentials).  
2. Click **Create Credentials → OAuth 2.0 Client ID**.  
3. Set **Application type** to `Web application`.  
4. Add **Authorized redirect URI**:

http://localhost:8080/login/oauth2/code/google

5. Copy **Client ID** and **Client Secret**.  
6. Set them as environment variables:

**Windows (PowerShell):**
```powershell
setx GOOGLE_CLIENT_ID "your-google-client-id"
setx GOOGLE_CLIENT_SECRET "your-google-client-secret"
Linux/Mac:

export GOOGLE_CLIENT_ID=your-google-client-id
export GOOGLE_CLIENT_SECRET=your-google-client-secret
Reference them in application.properties:

spring.security.oauth2.client.registration.google.client-id=${GOOGLE_CLIENT_ID}
spring.security.oauth2.client.registration.google.client-secret=${GOOGLE_CLIENT_SECRET}
spring.security.oauth2.client.registration.google.scope=openid,profile,email
2️⃣ GitHub OAuth2 Setup
Go to GitHub → Settings → Developer settings → OAuth Apps.

Click New OAuth App.

Set Application name and Homepage URL (http://localhost:8080).

Add Authorization callback URL:

http://localhost:8080/login/oauth2/code/github
Copy Client ID and Client Secret.

Set them as environment variables:

Windows (PowerShell):

setx GITHUB_CLIENT_ID "your-github-client-id"
setx GITHUB_CLIENT_SECRET "your-github-client-secret"
Linux/Mac:

export GITHUB_CLIENT_ID=your-github-client-id
export GITHUB_CLIENT_SECRET=your-github-client-secret
Reference them in application.properties:

spring.security.oauth2.client.registration.github.client-id=${GITHUB_CLIENT_ID}
spring.security.oauth2.client.registration.github.client-secret=${GITHUB_CLIENT_SECRET}
spring.security.oauth2.client.registration.github.scope=user:email
💡 OAuth2 Authentication Flow Overview
User clicks login via Google or GitHub.

Spring Security redirects the user to the respective OAuth2 provider.

User authenticates on Google/GitHub.

OAuth2 provider redirects back to:

http://localhost:8080/login/oauth2/code/{provider}
Spring Security creates a session for the authenticated user.

Secured endpoints now require the user to be logged in; OAuth2 session is automatically handled.

✅ Notes
Keep application.properties with real secrets out of GitHub; add it to .gitignore.

Provide a template application.properties.example for others to copy.

Test the login flow in incognito mode to avoid cached sessions.
