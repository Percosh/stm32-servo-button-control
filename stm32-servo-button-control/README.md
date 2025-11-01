# STM32F103_SERVO_BUTTON_CONTROL

Bu projede **STM32F103C8T6** mikrodenetleyicisi kullanılarak iki buton ile bir servo motorun PWM sinyal genişliği kontrol edilmiştir.  
Servo motorun konumu **TIM1 CH2 (PA9)** pininden verilen PWM darbesinin genişliğinin artırılıp azaltılması ile ayarlanır.

- **PB12** butonuna basıldığında servo **sola döner** (darbe genişliği azalır)
- **PA10** butonuna basıldığında servo **sağa döner** (darbe genişliği artar)

Darbe genişliği **500 ile 2500** arasında sınırlandırılmıştır.

---

## Demo

Aşağıdaki kısa video projeyi çalışırken göstermektedir:

https://github.com/Percosh/stm32-servo-button-control/releases/download/v1.0/stm32-servo-button-control.mp4

---

## ⚙️ Donanım Bilgileri

| Bileşen | Pin / Model |
|--------|-------------|
| Mikrodenetleyici | STM32F103C8T6 (PinARM Eğitim Kiti) |
| PWM Çıkışı | **PA9** (TIM1 CH2) |
| Sol Dönme Butonu | **PB12** |
| Sağ Dönme Butonu | **PA10** |
| Güç | USB (Kart üzerinden) |

> Not: Eğitim kitinde USB gücü yeterli. Harici projelerde **servo için ayrı 5V** + **ortak GND** önerilir.

---

## 🧠 Çalışma Mantığı

Servo motor konumu PWM darbe genişliğine bağlıdır:

| Konum (Yaklaşık) | PWM Darbe (us) |
|------------------|----------------|
| Minimum açı       | ~500 µs        |
| Orta (90° civarı) | ~1500 µs       |
| Maksimum açı      | ~2500 µs       |

Bu projede servo açısı **doğrudan pulse genişliği** değeri üzerinden kontrol edilir.  
Butonlar basılı tutuldukça pulse değeri **10 birim** artar veya azalır.

---

## 🧩 PWM Başlatma

```c
/* USER CODE BEGIN 2 */
HAL_TIM_PWM_Start(&htim1, TIM_CHANNEL_2);

uint16_t angle = 1500; // Başlangıç orta konum
/* USER CODE END 2 */


