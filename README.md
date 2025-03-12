# Java UnsupportedClassVersionError

## 📌 Masalah
Saat menjalankan file Java di **CMD**, muncul error:

```sh
PS D:\java> java HelloWorld
Exception in thread "main" java.lang.UnsupportedClassVersionError: HelloWorld has been compiled by a more recent version of the Java Runtime (class file version 67.0), this version of the Java Runtime only recognizes class file versions up to 52.0
    at java.lang.ClassLoader.defineClass1(Native Method)
    at java.lang.ClassLoader.defineClass(Unknown Source)
    at java.security.SecureClassLoader.defineClass(Unknown Source)
    at java.net.URLClassLoader.defineClass(Unknown Source)
    at java.net.URLClassLoader.access$100(Unknown Source)
    at java.net.URLClassLoader$1.run(Unknown Source)
    at java.net.URLClassLoader$1.run(Unknown Source)
    at java.security.AccessController.doPrivileged(Native Method)
    at java.net.URLClassLoader.findClass(Unknown Source)
    at java.lang.ClassLoader.loadClass(Unknown Source)
    at sun.misc.Launcher$AppClassLoader.loadClass(Unknown Source)
    at java.lang.ClassLoader.loadClass(Unknown Source)
    at sun.launcher.LauncherHelper.checkAndLoadMain(Unknown Source)
PS D:\java>
```

### 🔍 Penyebab
- **Kode dikompilasi dengan JDK lebih baru** (mis. JDK 13 → `class file version 67.0`).
- **Kode dijalankan dengan JRE lebih lama** (mis. JRE 8 → hanya mendukung `class file version 52.0`).

## 🛠 Solusi

### 1️⃣ **Cek Versi Java**
Cek versi yang digunakan dengan:
```sh
java -version
javac -version
```
Jika `javac` lebih tinggi dari `java`, berarti JRE terlalu lama.

### 2️⃣ **Kompilasi dengan Versi yang Sesuai**
Jika tetap ingin menggunakan JRE lama, kompile dengan:
```sh
javac --release 8 HelloWorld.java
```
Atau:
```sh
javac -target 8 -source 8 HelloWorld.java
```
Lalu jalankan kembali:
```sh
java HelloWorld
```

### 3️⃣ **Update JRE atau Gunakan Versi yang Sama**
- **Perbarui JRE** agar sesuai dengan JDK.
- **Unduh JDK terbaru** dari [Oracle](https://www.oracle.com/java/technologies/javase-downloads.html) atau [OpenJDK](https://openjdk.org/).

### 4️⃣ **Cek dan Atur Path Java**
Periksa apakah sistem masih menggunakan **JRE lama**:
```sh
where java
where javac
```
Jika masih menggunakan JRE lama, atur ulang **PATH** agar mengarah ke JDK yang lebih baru.

## 🎯 Kesimpulan
**Error terjadi karena perbedaan versi JDK saat kompilasi dan JRE saat eksekusi.**

✔ **Solusi cepat**: Kompilasi dengan `--release 8` jika JRE yang digunakan adalah Java 8.
✔ **Solusi permanen**: Perbarui JRE atau pastikan **`java` dan `javac` menggunakan versi yang sama**.

🚀 Semoga bermanfaat!

