# 🚀 Run a Simple Java Maven Build Job in Jenkins

## 🎯 Objective
Learn how to use Jenkins to build a simple Java application using Maven — your first step into CI/CD.

---

## 🛠️ Tools Required
- **Jenkins** (Installed locally or via Docker)
- **Java JDK** (8 or 11)
- **Apache Maven**
- **Git** (Optional — can run from local folder)

---

## 📁 Project Structure

```
hello-java-maven/
├── pom.xml
└── src/
    └── main/
        └── java/
            └── HelloWorld.java
```

---

## 📦 Step-by-Step Implementation

### ✅ Step 1: Create a Java HelloWorld App

**📄 src/main/java/HelloWorld.java**
```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, Jenkins + Maven!");
    }
}
```

### ✅ Step 2: Create a `pom.xml` File

**📄 pom.xml**
```xml
<project>
  <modelVersion>4.0.0</modelVersion>

  <groupId>com.example</groupId>
  <artifactId>hello</artifactId>
  <version>1.0</version>

  <build>
    <plugins>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-compiler-plugin</artifactId>
        <version>3.8.1</version>
        <configuration>
          <source>1.8</source>
          <target>1.8</target>
        </configuration>
      </plugin>
    </plugins>
  </build>
</project>
```

---

### ✅ Step 3: Start Jenkins Using Docker

```bash
docker run -p 8080:8080 -v jenkins_home:/var/jenkins_home jenkins/jenkins:lts
```

Access Jenkins at: [http://localhost:8080](http://localhost:8080)

Unlock Jenkins using the password from:
```bash
docker exec -it <container_id> cat /var/jenkins_home/secrets/initialAdminPassword
```

---

### ✅ Step 4: Configure Maven in Jenkins

1. Navigate to: `Manage Jenkins` → `Global Tool Configuration`
2. Under **Maven**, click **Add Maven**:
   - Name: `Maven-3.8.6`
   - ✔ Install Automatically
   - Version: `3.8.6`
3. Click **Save**

---

### ✅ Step 5: Create Jenkins Freestyle Project

1. Go to Dashboard → **New Item**
2. Name: `hello-java-maven-job`
3. Select **Freestyle Project** → Click OK

---

### ✅ Step 6: Configure Build Job

- In **Build Section**:
  - Click **Add Build Step** → **Invoke top-level Maven targets**
  - Set:
    - **Maven Version**: `Maven-3.8.6`
    - **Goals**: `clean package`

- (Optional) Under Build Environment:
  - ✔️ Delete workspace before build starts

---

### ✅ Step 7: Build the Job

1. Click **Build Now**
2. Click on the Build Number → **Console Output**
3. You should see:
```
[INFO] BUILD SUCCESS
```

---

## 📸 Sample Screenshots

### 🎯 Jenkins Job Configuration
![Jenkins Job Config](./screenshots/job-config.png)

### 🎯 Build Console Output
![Build Success](./screenshots/build-success.png)

---

## ✅ Deliverables

- ✅ `HelloWorld.java`
- ✅ `pom.xml`
- ✅ Jenkins Freestyle Job Configured
- ✅ Screenshot of Successful Build Output

---

## 💡 Bonus Tip

To make it CI-ready in a Git project:

```bash
git init
git add .
git commit -m "Initial Java Maven project for Jenkins CI"
```

Then connect your GitHub repo in Jenkins → SCM section.

---

## 🏁 Result

You now have a working CI pipeline using Jenkins + Maven to build a Java application! 🎉

