### RSCUAD Development Rules

    | RSCUAD 2021
    | danu andrean


peraturan ini dibuat dikarenakan banyaknya penambahan baris program dan pengembangan
robot disetiap tahun yang membuat program cukup berantakan, maka rule ini digunakan untuk mencoba
melakukan perubahan format program sesui dengan format dari 
<a href="https://emanual.robotis.com/docs/en/platform/op/getting_started/">Darwin-OP</a>
sehingga program akan lebih mudah
dianalisis dan rapi saat dilakukan penambahan kode secara masif.

#### --- Whitespace (tab)
Aturan pertama yang harus diikuti semua orang adalah menggunakan 'tab'
karakter, dan tidak menggunakan spasi, untuk membuat indentasi kode. Juga, 'tab'
karakter harus mewakili 4 spasi. 

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

#### --- formatting
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
        
 ## NOTE
 > jika melihat program tidak sesuai format, maka pengembang wajib memperbaiki dan mengkompile terlebih dahulu selanjutkan melakukan update commit dengan nama "format adjustment" dengan cara sebagai berikut.
 
        git add .
        git commit -m "# format adjustment"
        git push origin master
        
    
        
[![wiki](https://img.shields.io/badge/R--SCUAD-wiki-brightgreen?style=plactic&logo=wikipedia)](https://github.com/rscuad/wiki/wiki)
