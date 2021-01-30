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

Artik sistemimize kurabiliriz. Kutuphane dosyalari /usr/local/lib'e, include dosyalari ise /usr/local/include dizinine gidecektir. Bunun icin

    sudo make install

komutunu calistirmak yeterli olacaktir.


Ornek Uygulama
--------------

Yukarida yazilip sisteme kurulan kutuphaneyi kullanan uygulamayi yazacagiz. Yukarida yapilan kurulum islemi (make install) sonrasinda, header dosyasi /usr/local/include dizinine kopyalanmistir. Asagidaki ornekte oldugu gibi kullanabiliriz: 

    #include <compute.hpp>
    #include <iostream>

    using namespace std;
    int main(){
       double carpim;
       cout << multiply(10,20) << endl;
       return 0;
    }


Derlemek icin yine bir CMakeLists.txt dosyasi gerekecektir.

    cmake_minimum_required(VERSION 3.9)
    project(mylib_app VERSION 0.0.1 DESCRIPTION "app using mylib")
    set (CMAKE_CXX_STANDARD 17)
    find_library(MYLIB mylib)
    aux_source_directory(. SRC_LIST)
    add_executable(${PROJECT_NAME} ${SRC_LIST})
    TARGET_LINK_LIBRARIES(${PROJECT_NAME}  ${MYLIB})

CMakeLists.txt dosyasinda find_library satirina dikkat edin. Burada, sisteme kurulu olan mylib kutuphanesini kullanmasini soyluyoruz. En alt satirdaki TARGET_LINK_LIBRARIES ile de ana uygulamamiz ile hangi kutuphanelerin birlikte link edilecegini belirtiyoruz.


Uygulamayi derlemek icin, yine bir build dizini olusturalim:

    mkdir build
    cd build
    cmake ..

Simdi derlemeye haziriz:

    make

Bu islemden sonra, mylib_app calistirilabilir dosyasi hazirdir. ldd ile, uygulamanin gereksinim duydugu kutuphaneleri goruntuleriz:

    build$ ldd mylib_app 
	linux-vdso.so.1 (0x00007fffd6f4e000)
	libmylib.so.1 => /usr/local/lib/libmylib.so.1 (0x00007ff455746000)
	libstdc++.so.6 => /lib/x86_64-linux-gnu/libstdc++.so.6 (0x00007ff455577000)
	libm.so.6 => /lib/x86_64-linux-gnu/libm.so.6 (0x00007ff4553f4000)
	libgcc_s.so.1 => /lib/x86_64-linux-gnu/libgcc_s.so.1 (0x00007ff4553da000)
	libc.so.6 => /lib/x86_64-linux-gnu/libc.so.6 (0x00007ff455219000)
	/lib64/ld-linux-x86-64.so.2 (0x00007ff455752000)



Ciktinin ikinci satirinda libmylib.so.1 adini goreceksiniz. Boylece daha once yazmis oldugumuz kutuphaneyi, baska bir uygulama icinde kullanmis olduk.




