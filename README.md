### RSCUAD Development Rules

    | RSCUAD 2021
    | danu andrean


peraturan ini dibuat dikarenakan banyaknya penambahan baris program dan pengembangan
robot disetiap tahun yang membuat program cukup berantakan, maka rule ini digunakan untuk mencoba
melakukan perubahan format program sesui dengan format dari 
<a href="https://emanual.robotis.com/docs/en/platform/op/getting_started/">Darwin-OP</a>
sehingga program akan lebih mudah
dianalisis dan rapi saat dilakukan penambahan kode secara masif.

> kami merekomendasi menggunakan code editor <a href="https://code.visualstudio.com/">
  Visual Studio Code</a>
- [x] proses editing program dilakukan dikomputer pengembang jika dirobot tidak dianjurkan menggunakan vs code seperti odroid xu4.

#### --- Whitespace (tab)
Aturan pertama yang harus diikuti semua orang wajib menggunakan 'tab'
karakter, dan tidak menggunakan spasi, untuk membuat indentasi kode. <strong>Juga 'tab'
karakter harus mewakili 4 spasi.</strong>

#### --- Braces (kurung kurawal)
pada penggunakan kurung kurawal dilakukan dibawah pernyatan (if statement)
dan jika ditutup harus sejajar dengan awalan, contoh:

        if (error != -ENODEV) 
        {
            foo();
            bar();
        }
        
jika anda ingin menggunakan else statement, maka else statement tidak boleh sejajar 
dengan kurung kurawal sebagai berikut:

        if (error != -ENODEV) 
        {
            foo();
            bar();
        } 
        else 
        {
            report_error();
            goto exit;
        }
        
Jika kurung kurawal tidak diperlukan untuk sebuah pernyataan, jangan menggunakannya
karena itu tidak diperlukan, contoh:

        if (error != -ENODEV) 
            foo();
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

        int foo()
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
                        foo();
                }
            }
        }
        
#### --- Variable

varabel merupakan hal yang sering membuat struktur program berubah pada RSCUAD kita coba kembalikan
sesuai dengan Framework Darwin-OP yaitu menggunakan bahasa inggris dan nama yang sesuai dengan kepeluan
variable

            const int threshold = 250;  
            float approach = 0;
            
 gunankan tepe data yang sesui dengan kebutuhan. jika hanya digunakan untuk trigger yang bernilai
 true dan falde maka cukup gunakan boolean;
 
            bool trig = false;
            
 --- OP3 style. 
 deskripsikan varible pada header library program, kemudian deskripsikan nilai pada contruction library <a href="https://www.w3schools.com/cpp/cpp_constructors.asp">lihat disini</a>
 
 file header.h
 
            class header {        
                public: 
                    .....
                    .....
                private:
                    int y_axis; 
                    int x_axis; 
            };
        
        
 file header.cpp
 
            int header::header()
            {
                y_axis = 0;
                x_axis = 0;
            }
       
 
 
#### --- Commant
komentar digunakan untuk mendeskripsikan algoritma atau program yang kondisinya perlu dideskripsikan
gunakan perintah /* ...  untuk mendiskripsikan suatu algoritma tertentu dan // untuk variable.

            const int threshold = 250;  // const digunakan untuk nilai ketetapan
            float approach = 0;         // konstanta nilai awal
            
            /*
            *   algoritma dribling
            */
            if(pan != threshold)
                foo();
                
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

            void foo()
            {
                X_MOVE_AMPLITUDE = 10;
                Y_MOVE_AMPLITUDE = 15;
            }
            ....
            int main()
            {
                ......
                foo();
            }
            
            
#### --- GIT
<a href="https://git-scm.com/">GIT</a> adalah sebuah vcs(version control system) digunakan
untuk melakukan log dan kolaborasi dalam tim. Tutorial git dapat dilihat <a href="https://medium.com/@fahmiprasetiiio/belajar-git-untuk-pemula-7625c686c68f">
disini.</a>
<pre> -- pengembangan robot untuk mode
jika melakukan pengembangan robot dengan mode2 tertentu untuk pertandingan yang sama. pengembang 
diharuskan menggunakan branch untuk membuat environment sendiri sehingga tidak ada perubahan saat
melakukan pengembangan dimode lain.
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
