# RTOS Exercise 7 

Proyek ini adalah implementasi multitasking pada mikrokontroler STM32 dengan menggunakan FreeRTOS untuk mengendalikan tiga LED dengan interval waktu yang berbeda dan mengelola data bersama antara beberapa task.

## Cara Kerja 
1. Task HijauLedTask
* Mengontrol LED hijau dengan interval 200 ms. Task ini berfungsi untuk menyalakan dan mematikan LED hijau, mengakses data bersama (startFlag) secara aman, dan memastikan tidak ada konflik dengan task lain. 
* LED hijau menyala, lalu mengakses data bersama dengan aman. Setelah selesai, LED dimatikan, dan task tidur selama 200 ms (osDelay(200)).
2. Task MerahLedTask
* Mengontrol LED merah dengan interval 550 ms. Task ini bekerja hampir sama dengan HijauLedTask, tetapi LED yang dikendalikan adalah LED merah.
* LED merah menyala, mengakses data bersama, dan dimatikan setelah 550 ms (osDelay(550)).
3. Task OrangeLedTask
* Mengontrol LED oranye dengan interval 50 ms. Task ini memiliki prioritas lebih tinggi (osPriorityAboveNormal), sehingga akan lebih sering dieksekusi dibandingkan dengan task hijau dan merah.
* LED oranye akan berkedip setiap 50 ms, karena task ini memiliki prioritas lebih tinggi, maka akan terus berjalan dengan interval yang lebih singkat dibandingkan task lainnya.
4. Akses Data Bersama
* Variabel startFlag digunakan untuk menunjukkan status akses data bersama. Variabel ini dilindungi dengan critical section menggunakan taskENTER_CRITICAL() dan taskEXIT_CRITICAL(), untuk memastikan hanya satu task yang dapat mengakses data bersama pada satu waktu.
* Fungsi accessSharedData() bertanggung jawab untuk mengubah nilai startFlag dan menyimulasikan operasi baca/tulis. Selama operasi ini berlangsung, akses ke data bersama lainnya diblokir untuk menghindari konflik antar task.

## Hardware 

## Output Proyek 
* LED hijau akan menyala selama 200 ms, kemudian mati selama 200 ms secara bergantian.
LED ini akan melakukan siklus ini secara terus-menerus, diatur oleh task dengan interval 200 ms.
* LED merah akan menyala selama 550 ms, kemudian mati selama 550 ms.
LED merah akan beroperasi secara paralel dengan LED hijau, tetapi dengan siklus lebih panjang (550 ms) karena task ini memiliki waktu eksekusi yang lebih lama.
* LED oranye akan berkedip setiap 50 ms, karena task ini memiliki prioritas lebih tinggi. LED oranye akan menyala dan mati lebih sering dibandingkan dengan LED hijau dan merah.
