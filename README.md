<h1 class="code-line" data-line-start=0 data-line-end=1 ><a id="Sistem_Monitoring_Kehadiran_berbasis_ESP32Cam_dan_Sensor_PIR_0"></a>Sistem Monitoring Kehadiran berbasis ESP32-Cam dan Sensor PIR</h1>
<h2 class="code-line" data-line-start=1 data-line-end=2 ><a id="1_Menghubungkan_ESP32Cam_Dengan_UART_1"></a>1. Menghubungkan ESP32-Cam Dengan UART</h2>
<p class="has-line-data" data-line-start="2" data-line-end="3">Dalam merancang Sistem Monitoring Kehadiran berbasis ESP32-Cam dan Sensor PIR, dibutuhkan Universal Asynchronous Receiver/Transmitter atau UART yang digunakan untuk mengupload program ke ESP32-Cam. Berikut merupakan rangkain skematik untuk menghubungkan ESP32-Cam dengan UART.</p>
<img width="770" alt="Wiring_ESP32-CAM_TTL_USB" src="https://github.com/user-attachments/assets/b1790991-d742-48ce-9601-05162cde3f0c">
<h2 class="code-line" data-line-start=6 data-line-end=7 ><a id="2_Merangkai_ESP32Cam_Dengan_Sensor_PIR_6"></a>2. Merangkai ESP32-Cam Dengan Sensor PIR</h2>
<p class="has-line-data" data-line-start="7" data-line-end="9">Setelah ESP32-Cam terhubung dengan UART, langkah selanjutnya adalah menghubungkan ESP32-Cam dengan Sensor PIR. Sensor PIR akan mendeteksi pergerakan, dan ESP32-Cam akan mengambil gambar saat gerakan terdeteksi. Berikut adalah langkah-langkah merangkai ESP32-Cam dengan Sensor PIR menggunakan pin yang telah ditentukan:<br>
<img width="852" alt="Wiring_ESP32-CAM_dan_Sensor_PIR" src="https://github.com/user-attachments/assets/96fd013e-987b-4f1b-bc24-cd58f5dbab56">
<ol>
<li class="has-line-data" data-line-start="9" data-line-end="10">PIR SENSOR OUT PIN ke GPIO 12 (ESP32-Cam): Sambungkan pin OUT dari Sensor PIR ke pin GPIO12 pada ESP32-Cam. Pin ini akan mengirimkan sinyal saat gerakan terdeteksi.</li>
<li class="has-line-data" data-line-start="10" data-line-end="11">PIR SENSOR GND PIN ke GND (ESP32-Cam): Sambungkan pin GND dari Sensor PIR ke pin GND pada ESP32-Cam untuk menyelesaikan rangkaian daya.</li>
<li class="has-line-data" data-line-start="11" data-line-end="13">PIR SENSOR VCC PIN ke VCC (ESP32-Cam): Sambungkan pin VCC dari Sensor PIR ke pin VCC pada ESP32-Cam untuk memberikan daya ke Sensor PIR.</li>
</ol>
<h2 class="code-line" data-line-start=13 data-line-end=14 ><a id="3_Upload_Program_Ke_ESP32Cam_13"></a>3. Upload Program Ke ESP32-Cam</h2>
<p class="has-line-data" data-line-start="14" data-line-end="15">Langkah berikutnya dalam perancangan Sistem Monitoring Kehadiran ini adalah mengupload program ke ESP32-Cam dan melakukan modifikasi pada kode agar ESP32-Cam terhubung ke Bot Telegram serta menggunakan koneksi hotspot dari smartphone. Sebelum memulai, pastikan Anda telah menyiapkan bot Telegram melalui BotFather.</p>
<h3 class="code-line" data-line-start=15 data-line-end=16 ><a id="Buat_Bot_Telegram_melalui_BotFather_15"></a>Buat Bot Telegram melalui BotFather</h3>
<ol>
<li class="has-line-data" data-line-start="16" data-line-end="17">Buka aplikasi Telegram, dan cari BotFather menggunakan link: <a href="https://t.me/BotFather">https://t.me/BotFather</a>.</li>
<li class="has-line-data" data-line-start="17" data-line-end="18">Ketik /newbot dan ikuti langkah-langkah untuk membuat bot baru.</li>
<li class="has-line-data" data-line-start="18" data-line-end="19">Setelah berhasil membuat bot, BotFather akan memberikan Bot Token. Simpan token ini karena akan digunakan dalam program ESP32-Cam.</li>
</ol>
<h3 class="code-line" data-line-start=19 data-line-end=20 ><a id="Persiapan_Hotspot_19"></a>Persiapan Hotspot</h3>
<ol>
<li class="has-line-data" data-line-start="20" data-line-end="21">SSID dan Password Hotspot</li>
<li class="has-line-data" data-line-start="21" data-line-end="22">Simpan SSID dan Password untuk digunakan dalam program ESP32-Cam.</li>
</ol>
<h3 class="code-line" data-line-start=22 data-line-end=23 ><a id="Install_Board_ESP32_di_Arduino_IDE_22"></a>Install Board ESP32 di Arduino IDE</h3>
<ol>
<li class="has-line-data" data-line-start="23" data-line-end="24">Buka Arduino IDE.</li>
<li class="has-line-data" data-line-start="24" data-line-end="25">Pergi ke File &gt; Preferences.</li>
<li class="has-line-data" data-line-start="25" data-line-end="26">Pada bagian Additional Board Manager URLs, masukkan URL berikut: <a href="https://dl.espressif.com/dl/package_esp32_index.json">https://dl.espressif.com/dl/package_esp32_index.json</a></li>
<li class="has-line-data" data-line-start="26" data-line-end="27">Klik OK.</li>
<li class="has-line-data" data-line-start="27" data-line-end="28">Pergi ke Tools &gt; Board &gt; Boards Manager.</li>
<li class="has-line-data" data-line-start="28" data-line-end="29">Cari ESP32 dan klik Install pada library ESP32 by Espressif Systems.</li>
<li class="has-line-data" data-line-start="29" data-line-end="30">Kemudian install libary Telegram dan ESP32-Cam dengan Pergi ke Sketch &gt; Include Library &gt; Manage Libraries.</li>
<li class="has-line-data" data-line-start="30" data-line-end="31">Cari dan install library berikut: UniversalTelegramBot dan ESP32-CAM</li>
</ol>
<h3 class="code-line" data-line-start=31 data-line-end=32 ><a id="Upload_Kode_ke_ESP32CAM_31"></a>Upload Kode ke ESP32-CAM</h3>
<p class="has-line-data" data-line-start="32" data-line-end="33">Setelah library dan board berhasil diinstall, dan program sudah dimodifikasi sesuai kebutuhan, Anda dapat mengupload kode ke ESP32-CAM. Pastikan Anda telah mengganti “Token Bot Telegram”, “SSID”, dan “Password” hotspot sesuai dengan yang telah disiapkan sebelumnya.</p>
<h1 class="code-line" data-line-start=34 data-line-end=35 ><a id="Hasil_34"></a>Hasil</h1>
<p class="has-line-data" data-line-start="35" data-line-end="37">Sistem berjalan dengan baik, di mana ketika ada objek yang terdeteksi oleh sensor PIR, ESP32-CAM akan mengambil gambar dan memberikan isyarat flash yang menandakan bahwa gambar sedang diambil. Berikut adalah gambar rangkaian alat dan proses pengiriman gambar ke Telegram.<br>
<img src="https://github.com/user-attachments/assets/295d6df3-d9b2-4933-9f5f-99231f530674" alt="Screenshot 2024-09-21 211542"></p>
<p class="has-line-data" data-line-start="38" data-line-end="39">Baiklah, itu adalah proyek yang dapat saya bagikan kali ini. Jika ada teman-teman yang memiliki pertanyaan atau ingin mendiskusikan lebih lanjut, jangan ragu untuk menghubungi saya melalui link di bawah ini.</p>
<ul>
<li class="has-line-data" data-line-start="20" data-line-end="21">Instagram: <a href="https://www.instagram.com/_dhan.i/">_dhan.i</a></li>
<li class="has-line-data" data-line-start="22" data-line-end="23">LinkedIn: <a href="https://www.linkedin.com/in/ramadhani-aulia/">Aulia Ramadhani</a></li>
</ul>
