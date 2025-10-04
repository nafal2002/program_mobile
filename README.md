
```markdown
# Aplikasi Login & Register dengan C++ (Qt Framework)

Proyek ini merupakan implementasi form autentikasi (Login dan Register) yang dirancang dengan antarmuka pengguna (UI) modern menggunakan bahasa C++ dan Qt Framework. Aplikasi ini dikembangkan sebagai bagian dari tugas Ujian Tengah Semester (UTS) mata kuliah Pemrograman Mobile.

> **Catatan:** Penggunaan C++ untuk pengembangan aplikasi mobile dengan UI native tidak umum. Proyek ini memanfaatkan Qt Framework, salah satu solusi utama untuk membangun aplikasi GUI cross-platform dengan C++.

## 🚀 Fitur

-   Halaman **Login** dengan form input username dan password.
-   Halaman **Register** untuk pembuatan akun pengguna baru.
-   Navigasi yang halus antar halaman menggunakan `StackView`.
-   Desain UI yang responsif dan menarik dengan QML.
-   Pemisahan yang jelas antara logika bisnis (C++) dan antarmuka (QML).

## 👤 Informasi Pembuat

| Informasi | Detail |
|---|---|
| **Nama** | Nafal Mumtaz Fuadi |
| **NIM** | 312110457 |
| **Kelas** | TI.21.A.2 |
| **Universitas** | Universitas Pelita Bangsa |

## 📋 Prasyarat

Sebelum menjalankan proyek ini, pastikan lingkungan pengembangan Anda telah memenuhi syarat berikut:

1.  **Qt Framework**: Versi 6.x atau lebih baru yang telah terinstal. Unduh dari [situs resmi Qt](https://www.qt.io/download).
2.  **Qt Creator**: IDE resmi dari Qt untuk pengembangan aplikasi (biasanya sudah terinstal bersama Qt).
3.  **Kompiler C++**: Seperti MinGW (Windows), Clang (macOS), atau GCC (Linux).
4.  **Qt for Mobile**: Pastikan Anda telah menginstal komponen Qt untuk Android dan/atau iOS.

## 🛠️ Panduan Instalasi & Menjalankan

Ikuti langkah-langkah berikut untuk menjalankan proyek ini di lokal mesin Anda:

1.  **Kloning Repository**
    ```bash
    git clone https://github.com/username-anda/login_register_cpp.git
    cd login_register_cpp
    ```

2.  **Buka Proyek di Qt Creator**
    - Buka Qt Creator.
    - Pilih `File > Open File or Project...`.
    - Arahkan ke folder proyek dan pilih file `CMakeLists.txt` atau file `.pro`.

3.  **Konfigurasi & Build**
    - Pilih kit kompilasi yang sesuai (misalnya, Desktop, atau Android jika ingin menguji di emulator).
    - Klik tombol "Configure Project" jika muncul.
    - Build proyek dengan menekan `Ctrl+B` atau klik tombol Build.

4.  **Jalankan Aplikasi**
    - Jalankan aplikasi dengan menekan `Ctrl+R` atau klik tombol Run.

---

## 📖 Panduan Pembuatan (Dokumentasi Kode)

Bagian ini menjelaskan langkah demi langkah bagaimana aplikasi ini dibangun dari awal menggunakan C++ dan Qt.

### 1. Inisialisasi Proyek Qt

Buat proyek Qt baru di Qt Creator. Pilih template **Application (Qt Quick)**. Template ini menggunakan QML untuk UI dan C++ untuk logika, yang cocok untuk proyek ini.

### 2. Konfigurasi Sumber Daya (Resources)

Qt menggunakan sistem file sumber daya (`.qrc`) untuk mengemas aset seperti gambar.

1.  Klik kanan pada proyek di panel "Projects" dan pilih `Add New... > Qt > Qt Resource File`.
2.  Beri nama `resources.qrc`.
3.  Klik kanan pada file `.qrc` dan pilih `Add Prefix`, lalu `Add Files` untuk menambahkan gambar (misalnya `logo.png`) ke dalamnya.

### 3. Pembuatan Konstanta Warna

Untuk menjaga konsistensi warna, buat file header C++ untuk mendefinisikan palet warna.

**Buat file:** `constants.h`
```cpp
#ifndef CONSTANTS_H
#define CONSTANTS_H

#include <QColor>

namespace ColorPalette {
    static const QColor primaryColor = QColor(82, 100, 232); // #5364e8
    static const QColor primaryDarkColor = QColor(96, 124, 191); // #607Cbf
    static const QColor underlineTextField = QColor(139, 151, 255); // #8b97ff
    static const QColor hintColor = QColor(204, 209, 255); // #ccd1ff
}

#endif // CONSTANTS_H
```

### 4. Pembuatan Halaman Login (UI dengan QML)

Antarmuka pengguna dibuat dengan QML, sebuah bahasa deklaratif.

**Buat file:** `qml/LoginView.qml`
```qml
import QtQuick 2.15
import QtQuick.Controls 2.15
import QtQuick.Layouts 1.15

Page {
    id: loginPage

    background: Rectangle {
        color: "#5364e8" // ColorPalette.primaryColor
    }

    ColumnLayout {
        anchors.fill: parent
        anchors.margins: 20
        spacing: 10

        Image {
            id: logo
            source: "qrc:/images/logo.png"
            Layout.alignment: Qt.AlignHCenter
            Layout.preferredHeight: 150
            Layout.preferredWidth: 150
        }

        Text {
            text: "Login Into App"
            color: "white"
            font.pixelSize: 20
            Layout.alignment: Qt.AlignHCenter
        }

        TextField {
            id: usernameField
            placeholderText: "Username"
            placeholderTextColor: "#ccd1ff"
            color: "white"
            background: Rectangle {
                color: "transparent"
                border.color: "#8b97ff"
                border.width: 1
                radius: 5
            }
            Layout.fillWidth: true
        }

        TextField {
            id: passwordField
            placeholderText: "Password"
            placeholderTextColor: "#ccd1ff"
            color: "white"
            echoMode: TextInput.Password
            background: Rectangle {
                color: "transparent"
                border.color: "#8b97ff"
                border.width: 1
                radius: 5
            }
            Layout.fillWidth: true
        }

        Button {
            text: "Login"
            Layout.fillWidth: true
            background: Rectangle {
                color: "white"
                radius: 20
            }
            contentItem: Text {
                text: parent.text
                color: "#5364e8"
                horizontalAlignment: Text.AlignHCenter
                verticalAlignment: Text.AlignVCenter
            }
            onClicked: {
                // Logika login akan dipanggil dari sini
                console.log("Login clicked")
            }
        }

        Text {
            text: "or"
            color: "white"
            Layout.alignment: Qt.AlignHCenter
        }

        Button {
            text: "Register"
            Layout.alignment: Qt.AlignHCenter
            background: Rectangle { color: "transparent" }
            contentItem: Text {
                text: parent.text
                color: "white"
                underline: true
            }
            onClicked: stackView.push("qrc:/qml/RegisterView.qml")
        }
    }
}
```

### 5. Pembuatan Halaman Register (UI dengan QML)

Strukturnya mirip dengan halaman login, tetapi dengan form yang sesuai.

**Buat file:** `qml/RegisterView.qml`
```qml
import QtQuick 2.15
import QtQuick.Controls 2.15
import QtQuick.Layouts 1.15

Page {
    id: registerPage

    background: Rectangle {
        color: "#5364e8"
    }

    ColumnLayout {
        anchors.fill: parent
        anchors.margins: 20
        spacing: 10

        // ... (logo dan judul serupa dengan LoginView) ...

        TextField {
            id: newUsernameField
            placeholderText: "Username"
            // ... (properti serupa) ...
            Layout.fillWidth: true
        }

        TextField {
            id: newPasswordField
            placeholderText: "Password"
            // ... (properti serupa) ...
            Layout.fillWidth: true
        }

        Button {
            text: "Register"
            Layout.fillWidth: true
            // ... (properti serupa) ...
            onClicked: {
                // Logika register akan dipanggil dari sini
                console.log("Register clicked")
            }
        }

        Button {
            text: "Back to Login"
            Layout.alignment: Qt.AlignHCenter
            // ... (properti serupa) ...
            onClicked: stackView.pop()
        }
    }
}
```

### 6. Konfigurasi Routing (Navigasi)

Navigasi dikelola dalam file QML utama (`main.qml`) menggunakan `StackView`.

**Modifikasi file:** `qml/main.qml`
```qml
import QtQuick 2.15
import QtQuick.Controls 2.15

ApplicationWindow {
    visible: true
    width: 360
    height: 640
    title: qsTr("Login Register C++")

    StackView {
        id: stackView
        anchors.fill: parent
        initialItem: "qrc:/qml/LoginView.qml" // Halaman awal
    }
}
```

### 7. Finishing & Logika Backend

Logika bisnis (seperti validasi input atau komunikasi dengan server) ditulis dalam C++. Anda dapat mengekspos fungsi C++ ke QML agar dapat dipanggil dari UI.

**Contoh `backend.h`:**
```cpp
#ifndef BACKEND_H
#define BACKEND_H

#include <QObject>
#include <QString>

class Backend : public QObject
{
    Q_OBJECT
public:
    explicit Backend(QObject *parent = nullptr);

public slots:
    Q_INVOKABLE bool login(const QString &username, const QString &password);
    Q_INVOKABLE bool register(const QString &username, const QString &password);

signals:
    void loginSuccess();
    void loginFailed();
};

#endif // BACKEND_H
```

File `backend.cpp` akan mengimplementasikan logika dari fungsi-fungsi tersebut. Objek `Backend` kemudian didaftarkan di `main.cpp` agar dapat diakses dari QML.

---

## 📝 Catatan Tambahan

-   Proyek ini mendemonstrasikan arsitektur dasar C++/QML. Untuk aplikasi produksi, logika autentikasi harus terhubung dengan backend yang aman.
-   Validasi input di sisi C++ sangat penting untuk mencegah error dan celah keamanan.

Semoga panduan ini bermanfaat!
```
