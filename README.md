C++ ile Kutuphane Olusturma
===========================

Kisaca c++ ile kutuphane olusturmaktan bahsedecegiz.
CMake kullanacagiz. Bilgisayarinizda kurulu degilse, 

    https://cmake.org/download/

adresinden cekebilirsiniz. Ya da kullandiginiz linux dagitiminin
depolarindan da kurabilirsiniz:

    sudo apt install cmake

    yum install cmake

    dnf install cmake

gibi.


Asagida CMakeLists.txt dosyasinin icerigi bulunmakta:

    cmake_minimum_required(VERSION 3.9)
    project(mylib VERSION 0.0.1 DESCRIPTION "mylib description")
    add_library(mylib SHARED
        sources/compute.cpp)
    set_target_properties(mylib PROPERTIES VERSION ${PROJECT_VERSION})


Repoyu

    git clone https://github.com/ilkermanap/cpp-library-create

komutu ile bilgisayariniza indirin.

    cd cpp-library-create

ile dizinin icine girin. Cmake ile calismak icin, build adinda bir dizin olusturun ve icine girin.

    mkdir build
    cd build

Derleme icin gerekli dosyalari olusturmak icin

    cmake ..

komutunu calistirin. Ardindan

    make

komutu ile derleme islemini yapabilirsiniz.  Derleme isleminin sonunda linux sistemlerde baska uygulamalari yazarken kullanabileceginiz bir so uzantili dosya olusmus olacaktir.
