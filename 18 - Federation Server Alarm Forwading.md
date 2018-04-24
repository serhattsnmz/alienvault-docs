## Federation Server Alarm Forwading

- Müşteri USM'ini Federation üzerine ekleme
    - Federation Server üzerinde;
    - `Configuration > Deployment > Servers` yoluna gidilir.
    - `New` tıklanarak yeni USM eklenir.
- Alarm Yönlendirmesi:
    - Müşteri USM üzerinde;
        - `Configuration > Deployment > Servers` yoluna gidilir.
        - Federation Server seçilip `Modify` işaretlenir.
        - Müşteri USM Admin panel bilgileri (` Remote Admin User, Remote Password, and Remote URL`) buraya girilir.
        - `Set Remote Key` tıklanıp kaydedilir.
    - Müşteri USM Üzerinden;
        - `Configuration > Deployment > Servers` yoluna gidilir.
        - Müşteri USM seçilip `Modify` işaretlenir.
            - `Forward Alarms > Yes`
            - `Forward Events > No` işaretlenir.
            - `Forward Servers` altından `Add Server` seçilip, Federation server seçildikten sonra `Add New` tıklanır.
            - `Priority` 1 olarak işaretlenir.
            - `Save` diyerek kaydedilir.