# Install Java 8/11/17 on Amazon Linux:-

[Credits: Check this URL for detailed info](https://tecadmin.net/install-java-on-amazon-linux/)

* As of now, Oracle has restricted these Java versions for registered users only, so we will use OpenJDK for this installation

### Step 1 – Install Java on Amazon Linux

The OpenJDK 8 is available under default yum repositories and OpenJDK 11 is available under Amazon Linux 2 extras repositories. You can simply install Java 11 or Java 8 on the Amazon Linux system using the following commands.

* Run below commands to install **Java 8** on Amazon Linux:
  
  ```shell
  yum install -y java-1.8.0-openjdk
  ```
* Run below commands to install **Java 11** on Amazon Linux:
  
  ```shell
  amazon-linux-extras install java-openjdk11
  ```
### Step 2 – Check Active Java Version

```shell
java -version
```
### Step 3 – Switch Java Version

Use alternatives command-line utility to switch active Java version on your Amazon Linux system. Run below command from the command line and select the appropriate Java version to make it default.

```shell
alternatives --config java
```

After switching let’s check again active Java version using **java -version**

---

# Java 17 Installation:

**yum install -y java-17-amazon-corretto-devel.x86_64**
