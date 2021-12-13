# teknolojikampi2021
Açıklab Pardus ve Liman Teknoloji Kampı

## Senaryo 

- Liman eklentisi geliştirilmesi
- Eklenti ile bir IP adresinin SNMP kullanılarak bandwith'inin takip edilmesi

### Inputs

- SNMP istemcisinin IP Adresi
- SNMP key string'i

### Output

- Belirtilen sunucunun bandwith'inin canlı grafiği 

## Bilgi

- Paylaşılan LAB bağlantıları, çoğunlukla half-duplex'tir. WAN bağlantıları full-duplex'tir.
- Formüllerde kullanılan değişkenler
  - DeltaIfImOctets: snmp ifInOctets objelerinin (gelen trafiği ifade eder) iki poll cycle (döngü) arasındaki farkı.
  - DeltaIfOutOctets: snmp ifOutOctets objelerinin (giden trafiği ifade eder) iki poll cycle (döngü) arasındaki farkı.
  - IfSpeed: snmpifSpeed objesi tarafından raporlanan arayüzün hızı

## Çözüm

- half-duplex formül:

  ```
  ((DeltaIfInOctets + DeltaIfOutOctets) * 8 * 100) / (saniye * IfSpeed)
  ```

- Full-duplex formül:

  ```
  (max(DeltaIfInOctets,DeltaIfOutOctets) * 8 * 100) / (saniye * IfSpeed)
  ```

- Sadece gelen trafik formül:

  ```
  (DeltaIfInOctets * 8 * 100) / (saniye * IfSpeed)
  ```

- Sadece giden trafik:

  ```
  (DeltaIfOutOctets * 8 * 100) / (saniye * IfSpeed)
  ```

- OID 1.3.6.1.2.1.2.2.1 yukarıdaki bilgileri içerir

  - ifInOctets  1.3.6.1.2.1.2.2.1.10
  - ifOutOctets  1.3.6.1.2.1.2.2.1.16
  - isSpeed ifInOctets  1.3.6.1.2.1.2.2.1.5

## Kaynaklar
- https://dev.to/aciklab/ubuntu-uzerinde-snmp-servisi-kurulumu-47d8
- https://docs.liman.dev/eklenti-gelistirme/