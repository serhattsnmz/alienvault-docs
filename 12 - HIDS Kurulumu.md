## HIDS KURULUMU

### 01 - Windows Host Üzerine HIDS Kurulumu

- `Environment > Detection` yoluna gidilir.
- `HIDS > Agents > Agent Control > Add Agent` tıklanır.
- Asset ağacı üzerinden host seçilir.
- `Save` tıklanarak kaydedilir. Bu şekilde yeni agent listeye eklenmiş olur.
- Agent'ı deploy etmek için sağ tarafındaki deploy tuşuna tıklanır.
- Otomatik deployment için `Domain`, `User` ve `Password` bilgileri girilip `Save` tıklanır.
- Alternatif olarak bu yapı manuel olarak da yapılabilir.
    - Öncelikle ilgili agent sağındaki download tuşuna basılır.
    - `ossec_installer_<agent_id>.exe` adlı bir dosya inecektir.
    - Bu dosya ilgili windows host üzerinde çift tıklanarak çalıştırılır.

### 02 - Linux Host Üzerine HIDS Kurulumu

- `Environment > Detection` yoluna gidilir.
- `HIDS > Agents > Agent Control > Add Agent` tıklanır.
- Asset ağacı üzerinden host seçilir.
- `Save` tıklanarak kaydedilir. Bu şekilde yeni agent listeye eklenmiş olur.
- Agent sağındaki tuşlardan anahtar olana tıklanır ve KEY kopyalanır.
- Linux host üzerinde `/var/ossec/bin/manage_agents` çalışrırılır ve `I` tuşuyla daha önce kopyalanan key buraya eklenir.
- `/var/ossec/etc/ossec-agent.conf` dosyası üzerinden server IP adresi `USM Appliance` IP adresi olarak değiştirilir.
- HIDS Agent çalışmıyorsa, çalıştırılır.

```
service ossec start
chkconfig ossec-hids on
```

- USM üzerinden `Environment > Detection` üzerinden `HIDS Control` seçilerek restart edilir.