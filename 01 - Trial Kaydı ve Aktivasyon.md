## Trial Kaydı ve Aktivasyon

- Trial kaydı için aşağıdaki web sitesinden kayıt olunur : 
    - https://www.alienvault.com/products/usm-appliance/free-trial
- Kayıt olduktan sonra çıkan sayfada imaj indirme linki mevcuttur. 
    - Eğer imaj indirme sorunu varsa, direk olarak şu linkten indirme yapılabilir.
    - https://dlcdn.alienvault.com/AlienVault-USM_trial.zip?t=15105306390995jstG01XlAfB

#### Demo süresini uzatma

- Yukarıda verilen trial kayıt adresinden farklı bir mail adresiyle kayıt yapılır.
- AlienVault üzerine SSH ile bağlantı yapılır.
- `Jailbreak` seçeneği seçilir.
- Konsol üzerinden aşağıdaki kod çalıştırılır.

```
alienvault-api register_appliance -t -k user@domain.tld
```