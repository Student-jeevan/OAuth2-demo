# OAuth2 Demo Application (Spring Boot)

This is a Spring Boot demo application showcasing **OAuth2 login integration** with Google and GitHub.  
Users can log in using their Google or GitHub accounts. The project uses **environment variables** to securely manage OAuth client credentials.

---

## 1️⃣ Spring Boot Configuration

1. Ensure you have **Java 17+** and **Maven** installed.  
2. Clone the repository:
```bash
git clone https://github.com/your-username/oauth2-demo.git
cd oauth2-demo
Set your environment variables (replace with your keys):
Windows (PowerShell):

setx GOOGLE_CLIENT_ID "your-google-client-id"
setx GOOGLE_CLIENT_SECRET "your-google-client-secret"
setx GITHUB_CLIENT_ID "your-github-client-id"
setx GITHUB_CLIENT_SECRET "your-github-client-secret"

Linux/Mac:

export GOOGLE_CLIENT_ID=your-google-client-id
export GOOGLE_CLIENT_SECRET=your-google-client-secret
export GITHUB_CLIENT_ID=your-github-client-id
export GITHUB_CLIENT_SECRET=your-github-client-secret

Run the application:
mvn spring-boot:run


Open the browser and navigate to:

http://localhost:8080
How to Add Google OAuth2
Go to Google Cloud Console → APIs & Services → Credentials

Click Create Credentials → OAuth 2.0 Client ID

Set Application type to Web application

Add Authorized redirect URI:

http://localhost:8080/login/oauth2/code/google
Copy the Client ID and Client Secret

Set them as environment variables (GOOGLE_CLIENT_ID and GOOGLE_CLIENT_SECRET)

Add to your application.properties as:

spring.security.oauth2.client.registration.google.client-id=${GOOGLE_CLIENT_ID}
spring.security.oauth2.client.registration.google.client-secret=${GOOGLE_CLIENT_SECRET}
spring.security.oauth2.client.registration.google.scope=openid,profile,email
3️⃣ How to Add GitHub OAuth2
Go to GitHub → Settings → Developer settings → OAuth Apps

Click New OAuth App

Set Application name and Homepage URL (http://localhost:8080)

Add Authorization callback URL:

http://localhost:8080/login/oauth2/code/github
Copy the Client ID and Client Secret

Set them as environment variables (GITHUB_CLIENT_ID and GITHUB_CLIENT_SECRET)

Add to your application.properties as:

spring.security.oauth2.client.registration.github.client-id=${GITHUB_CLIENT_ID}
spring.security.oauth2.client.registration.github.client-secret=${GITHUB_CLIENT_SECRET}
spring.security.oauth2.client.registration.github.scope=user:email
✅ Notes
Keep application.properties with real secrets out of GitHub; use .gitignore.

Provide a template application.properties.example for others to copy.

Test the login flow in incognito mode to avoid cached sessions.
