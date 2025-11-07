Лабораторна робота №3 i2c Виконав АС-31 Ніколаєнко А. Г. Варіант 7

1. Виконаємо конфігурацію пінів контроллера як зображено на рис. 1 і налаштуємо тактову частоту на 400 кГц (доступна тільки у режим Fast Mode).
   
   <img width="1331" height="663" alt="image" src="https://github.com/user-attachments/assets/6747120b-d06e-4366-bafa-3ffbd9c3f634" />

2. Підключимо датчик як зображено на малюнку. Слід зауважити, що датчик може бути підключеним до двох пристроїв одночасно, тому пін SDA слід підтянути або до землі, або то 3.3В живлення відповідно.

  ![IMG_1218](https://github.com/user-attachments/assets/80d42a8e-364f-4e65-8aa3-107b22358e8a)

  ![IMG_1223](https://github.com/user-attachments/assets/ba20074e-9873-4999-b525-fbe71da986e7)


3. Перейдемо до написанню кода, попередньо оголосивши необхідні змінні глобально.
   
   <img width="361" height="88" alt="image" src="https://github.com/user-attachments/assets/8cca6558-811b-4490-9133-a8b2e9af441f" />

4. За допомогою команди HAL_I2C_Mem_Read зчитаємо дані з регістру, де знаходиться унікальний ідентифікатор датчика. Він повинен мати значення 105'i'.
   Т.я. у маоєму варіанті заданий акселерометр то динамічні параметри датчика будемо задавати в сегментах регістра 0x10.
   У заданому варіанті Діапазон вимірювання(FS) = ±2 g, а Частота видачі інформації (ODR) = 833 Hz, отже відповідно до таблиці і схеми нижче значення змінної ctrl1_xl набуває значення 0x70.
   
   <img width="621" height="79" alt="image" src="https://github.com/user-attachments/assets/77c09a25-ff4a-409a-9941-c81f0fa4b01e" />
   
   <img width="617" height="362" alt="image" src="https://github.com/user-attachments/assets/8a27b5a6-6f19-4cd2-a459-be9810291492" />
   
   <img width="607" height="93" alt="image" src="https://github.com/user-attachments/assets/1526986d-3e59-4aad-9364-88cbeb4fc7f8" />

   ODR = ob0111;  FS = 0b00;  BW = 0b00;

   <img width="625" height="57" alt="image" src="https://github.com/user-attachments/assets/800f4936-5f8b-48fb-b0ec-6f784f7557a7" />

   5. Тепер, налаштувавши датчик, перейдемо до зчитування данних. Т.я. регістри мають 8-бітну структуру, а значення проекцій прискорень на осі - 16 бітні інтеджери, то дані зчитуємо з двох регістрів: 0x28 і 0x28 + sizeof(int16_t) - наступний регістр.
      Перший регістр записуємо в молодшу частину змінної, а другий - в старшу.  
  
      <img width="673" height="111" alt="image" src="https://github.com/user-attachments/assets/d875953b-6a39-44b1-891f-bd8e93df3f12" />
   6. Для отримання значення у реальних, а не квантованих одиницях, тобто в градусах, домножимо вихідні параметри на чутливість.

      <img width="471" height="71" alt="image" src="https://github.com/user-attachments/assets/10ecd7a2-cea1-439f-85d8-5f350b149928" />

   7. Для перевірки вихідних значень скористажмость функцією відлагоджування в STM32CubeIDE.
      
      https://github.com/user-attachments/assets/23bac95f-a203-497d-a41a-8a566d3da7b2
      






  


   


