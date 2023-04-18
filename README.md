### RSCUAD Development Rules

    | RSCUAD 2021
    | Rscuad Team


peraturan ini dibuat dikarenakan banyaknya penambahan baris program dan pengembangan
robot disetiap tahun yang membuat program cukup berantakan, maka rule ini digunakan untuk mencoba
melakukan perubahan format program sesui dengan format dari 
<a href="https://emanual.robotis.com/docs/en/platform/op/getting_started/">Darwin-OP</a>
sehingga program akan lebih mudah
dianalisis dan rapi saat dilakukan penambahan kode secara masif.

> kami merekomendasi menggunakan code editor <a href="https://code.visualstudio.com/">
  Visual Studio Code</a>
- [x] proses editing program dilakukan dikomputer pengembang jika dirobot tidak dianjurkan menggunakan vs code seperti odroid xu4.

#### --- Create New Program Robot
pisahkan research Rscuad dengan folder robot darwin OP2 dengan menggunakan submodule untuk library rscuad. tambahkan setiap research baru di dalam repo rscuad. penambahan hanya dilakukan dengan ijin ketua tim.

- clone folder base OP2

        $ git clone https://github.com/R-SCUAD-PROGRESS/rscuad-base.git
        $ cd rscuad-base

<b>anda dapat dengan mudah melakukan konfigurasi dengan melakukan perintah:</b>
        
        $ sudo chmod 777 setup.sh
        $ ./setup.sh

<b>dengan melakukan perintah diatas anda bisa mengabaikan settingan dibawah!</b>

- create submodule

        $ git submodule add <url> Rscuad

- update submodule

        $ cd Rscuad
        $ git pull origin master
        $ cd ..

- tampilan directory
        
        - rscuad-base 
            + Framework
            + Linux
            + Rscuad

- push program to github

        $ git add .
        $ git commit -m "add submodule"
        $ git push origin master
        
#### --- Configuration file
konfigurasi baru file rscuad

        rscuad-base 
            + Framework
            + Linux
            + Rscuad

jika anda ingin menambahkan fitur yang ada pada folder rscuad perbarui makefile sehingga file .cpp akan dapat dieksekusi    
        
        # add new files to redirect Rscuad folder
        RSCUAD_SRC  =   $(RSCUAD_DIR)/communication/communication.cpp\
                        $(RSCUAD_DIR)/serial/serial.cpp\
                        $(RSCUAD_DIR)/utilities/swap.cpp\
                        $(RSCUAD_DIR)/camera/camera.cpp
        
        ....

        $(TARGET): darwin.a $(OBJECTS)
	            $(CXX) $(CFLAGS) $(OBJECTS) $(RSCUAD_SRC) ../../lib/darwin.a -o $(TARGET) $(LFLAGS)
	            chmod 755 $(TARGET)

#### --- Create New Project
- masuk pada directory Linux/project buat nama baru dengan mengcopy folder soccer jika rule berubah
- jika tidak lakukan workflow pada folder yang sudah tersedia seperti dibawah
        
        + build
        + include
        + lib
        - project
            + Soccer            -> perlombaan offline / sepak bola normal
            + Technical         -> perlombaan Technical challenge
            ....

#### --- Whitespace (tab)
Aturan pertama yang harus diikuti semua orang wajib menggunakan 'tab'
karakter, dan tidak menggunakan spasi, untuk membuat indentasi kode. <strong>Juga 'tab'
karakter harus mewakili 4 spasi.</strong>

#### --- Case style
Gunakan Pascal case untuk class dan function, gunakan Camel case untuk variable <a href="https://betterprogramming.pub/string-case-styles-camel-pascal-snake-and-kebab-case-981407998841"> see referance</a>

#### --- Braces (kurung kurawal)
pada penggunakan kurung kurawal dilakukan dibawah pernyatan (if statement)
dan jika ditutup harus sejajar dengan awalan, contoh:

        if (error != -ENODEV) 
        {
            Foo();
            Bar();
        }
        
jika anda ingin menggunakan else statement, maka else statement tidak boleh sejajar 
dengan kurung kurawal sebagai berikut:

        if (error != -ENODEV) 
        {
            Foo();
            Bar();
        } 
        else 
        {
            report_error();
            goto exit;
        }
        
Jika kurung kurawal tidak diperlukan untuk sebuah pernyataan, jangan menggunakannya
karena itu tidak diperlukan, contoh:

        if (error != -ENODEV) 
            Foo();
        else 
            goto exit;

#### --- Formatting Statement
jika menggunakan terlalu banyak pernyatakan pastikan membuat fungsi baru pada sebelum fungsi main.
hal ini akan memudahkan pengeliatan dalam baris program untuk identifikasi, contoh jika mengalami 
hal seperti ini:
        
        int main()
        {
                .....
            if(state1)
            {
                if(state2)
                {
                    if(state3)
                    {
                        if(parameter_equation)
                        {
                            if(robot_equation)
                                //do something
                        }
                    }
                }
            }
        }


gunakan function untuk membuat program lebih rapi

        int Foo()
        {
            if(parameter_equation)
            {
                if(robot_equation)
                    //do something
            }
        }
         
        int main()
        {
            .....
            if(state1)
            {
                if(state2)
                {
                    if(state3)
                        Foo();
                }
            }
        }
        
#### --- Variable
variabel merupakan hal yang sering membuat struktur program berubah pada RSCUAD kita coba kembalikan
sesuai dengan Framework Darwin-OP yaitu menggunakan bahasa inggris dan nama yang sesuai dengan keperluan
variable

        const int threshold = 250;  
        float approach = 0;
            
gunankan tipe data yang sesui dengan kebutuhan. jika hanya digunakan untuk trigger yang bernilai
true dan false maka cukup gunakan boolean;
 
        bool trig = false;
            
#### --- Initial style. 
deskripsikan variable pada header library program, kemudian deskripsikan nilai pada construction library <a href="https://www.w3schools.com/cpp/cpp_constructors.asp">lihat disini</a>
 
 file header.h
 
        class Header 
        {        
            public: 
                .....
                .....
            private:
                int y_axis; 
                int x_axis; 
        };
        
        
 file header.cpp
 
        int Header::Header()
        : y_axis(0)
        , x_axis(0)
        {
        }
       
 
 
#### --- Comment
komentar digunakan untuk mendeskripsikan algoritma atau program yang kondisinya perlu dideskripsikan
gunakan perintah /* ...  untuk mendiskripsikan suatu algoritma tertentu dan // untuk variable. gunakan
komentar yang jelas pada setiap algoritma sehingga mudah dipahami. komentar diperbolehkan menggunkan bahasa indonesia.

        const int threshold = 250;  // const digunakan untuk nilai ketetapan
        float approach      = 0;    // konstanta nilai awal

        /*
         *   algoritma dribling
         */
        if(pan != threshold)
            Foo();
                
#### --- Pattern
gunakan pola <a href="https://en.wikipedia.org/wiki/Don%27t_repeat_yourself">DRY Principle</a> untuk mengurangi 
program yang tidak diperlukan. contoh menggunakan perulangan.

        /*
         *   Tidak disarankan
         */
        servo_pan = 5;
        servo_pan = 10;
        servo_pan = 15;
        servo_pan = 20;


        /*
         *   disarankan
         */
        for(int i=5; i<=20; i+5)
            servo_pan = i;
                
gunakan fuction atau library jika sebuah kondisi yang digunakan terus menerus

        void Foo()
        {
            X_MOVE_AMPLITUDE = 10;
            Y_MOVE_AMPLITUDE = 15;
        }
        ....
        int main()
        {
            ......
            Foo();
        }

            
#### --- GIT
<a href="https://git-scm.com/">GIT</a> adalah sebuah vcs(version control system) digunakan
untuk melakukan log dan kolaborasi dalam tim. Tutorial git dapat dilihat <a href="https://medium.com/@fahmiprasetiiio/belajar-git-untuk-pemula-7625c686c68f">
disini.</a>
<pre> -- pengembangan robot untuk mode
jika melakukan pengembangan robot dengan mode-mode tertentu untuk pertandingan yang sama. pengembang 
diharuskan menggunakan branch untuk membuat environment sendiri sehingga tidak ada perubahan saat
melakukan pengembangan di mode lain.
</pre>
    
        $ git branch mode2
        $ git checkout mode2
            
 hanya seperti itu. jika ingin melihat branch seperti ini:
 
        $ git branch
        >    master
           * mode2
               
 tanda * berarti project kita poda branch tersebut.
 
 
 ## NOTE
 > jika melihat program tidak sesuai format, maka pengembang wajib memperbaiki dan mengkompile 
 terlebih dahulu selanjutkan melakukan update commit dengan nama "format adjustment" dengan cara sebagai berikut.
 
        $ git add .
        $ git commit -m "# format adjustment"
        $ git push origin master
        
    
        
[![wiki](https://img.shields.io/badge/R--SCUAD-wiki-brightgreen?style=plactic&logo=wikipedia)](https://github.com/rscuad/wiki/wiki)
