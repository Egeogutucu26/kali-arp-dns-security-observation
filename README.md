# Kali Linux’ta ARP ve DNS Güvenliği: Gözlem ve Savunma

Bu depo, Kali Linux üzerinde **izole ve yetkili bir eğitim laboratuvarında** ARP ve DNS’in çalışma biçimini gözlemleme ve bu protokollere ilişkin temel savunma yaklaşımlarını belgeleme amacıyla hazırlanmıştır.

## Amaç

- ARP’nin yerel ağda IP adreslerini MAC adresleriyle nasıl eşleştirdiğini kavramsal olarak açıklamak.
- DNS sorgularının ad çözümlemedeki rolünü anlamak.
- Yalnızca laboratuvar ortamında, beklenen ağ davranışına ilişkin gözlemleri kaydetmek.
- Beklenmeyen ARP eşleştirmeleri veya DNS yanıtları için güvenli inceleme ve olay bildirim sürecini tanımlamak.

## Kapsam ve sınırlar

Çalışma, sahibine ait veya açık yazılı izin alınmış, internetten ve üretim ağlarından yalıtılmış sanal laboratuvarlarla sınırlıdır. Örnekler sentetik laboratuvar verileri üzerinden değerlendirilmelidir.

Bu depoda ARP/DNS sahteciliği uygulama, trafiği başka bir sisteme yönlendirme, gerçek ağ trafiğini yakalama, kimlik bilgisi toplama veya güvenlik kontrollerini aşmaya yönelik çalıştırılabilir adımlar bulunmaz.

## Güvenli laboratuvar ilkeleri

- Sanal makineleri host-only veya eşdeğer biçimde yalıtılmış bir sanal ağa bağlayın; köprülenmiş üretim/açık ağlarda test yapmayın.
- Gerçek kullanıcı verisi yerine sentetik laboratuvar trafiği kullanın.
- Laboratuvarı çalıştırmadan önce sanal makine anlık görüntüsü alın ve değişiklikleri test sonunda geri alın.
- Üçüncü taraf sistemlerinde deneme yapmayın; kapsam ve izin belirsizse çalışmayı durdurun.

## Savunma ve gözlem kontrol listesi

1. Yetkili ağda beklenen ağ geçidi ve DNS çözümleyicisi bilgisini önceden belgeleyin.
2. ARP eşleştirmelerinde veya DNS yanıtlarında beklenmeyen değişiklikleri güvenilir kayıtlarla karşılaştırın.
3. Şüpheli değişiklikleri zaman damgası ve laboratuvar bağlamıyla kaydedin; gerçek kullanıcı verilerini paylaşmayın.
4. Üretim ağlarında olay müdahalesi ve ağ yöneticisi süreçlerini izleyin; tek başınıza aktif müdahale denemesi yapmayın.

## Azaltım önerileri

- Uygun anahtarlarda DHCP snooping ve Dynamic ARP Inspection gibi katman-2 kontrollerini değerlendirin.
- Ağ segmentasyonu ve erişim denetimleri uygulayın; yönetim arayüzlerini sınırlandırın.
- DNS çözümleyici yapılandırmalarını yönetin, güvenilir çözümleyiciler kullanın ve DNS kayıtlarındaki beklenmeyen değişiklikleri izleyin.
- TLS/HTTPS doğrulamasını koruyun; sertifika uyarılarını atlamayın.
- Şüpheli olayları kurumsal güvenlik/olay müdahale ekibine bildirin.

## Etik ve sorumluluk

İçerik eğitim amaçlıdır ve bir güvenlik ürünü değildir. Herhangi bir testten önce sistem sahibinden açık izin ve net kapsam alın. Yetkisiz izleme veya müdahaleden doğabilecek sonuçlardan kullanıcı sorumludur.

## Güvenli terminal tanılama komutları

Aşağıdaki komutlar yerel arayüz, rota, komşu tablosu, yönlendirme ayarı ve DNS yapılandırmasını **görüntüler**; ağ trafiğini başka sisteme yönlendirmez veya yakalamaz. Yalnızca yetkili laboratuvar ortamında kullanın.

```bash
# Ağ arayüzleri ve IP adresleri
ip -br address

# Varsayılan ağ geçidi ve rotalar
ip route

# İşletim sisteminin bildiği yerel ARP/komşu tablosu
ip neigh show

# IPv4 forwarding ayarının mevcut değerini oku (değişiklik yapmaz)
sysctl net.ipv4.ip_forward

# DNS çözümleyici durumunu görüntüle (systemd-resolved bulunan sistemlerde)
resolvectl status

# Örnek bir alan adı için DNS çözümlemesini sorgula
dig example.com

# Eski net-tools paketi kuruluysa arayüz bilgilerini görüntüle
ifconfig
```

`netdiscover` gibi ağ keşif araçları başka cihazlarda sorgu oluşturabilir; ARP spoofing, DNS spoofing, paket yakalama ve trafik yönlendirme modülleri ise üçüncü taraf trafiğine müdahale edebilir. Bu nedenle bu depoda bunlara ilişkin çalıştırma komutları yayımlanmamıştır. Gereksinim duyulan her test için yazılı izin ve yalıtılmış laboratuvar kullanın.

## 9. ve 10. bölüm: ARP/DNS riskleri — savunma özeti

Bu ders notlarında ağ keşfi, IP yönlendirme, ARP tablosunun manipülasyonu, trafik gözlemi ve DNS yanıtlarının değiştirilmesi gibi riskli konular ele alınmaktadır. Bu teknikler izinsiz kullanıldığında trafiğin yönünü değiştirebilir veya özel ağ verilerini açığa çıkarabilir. Bu nedenle burada çalıştırılabilir saldırı zinciri, eksik parametre tamamlama ya da trafik yakalama yönergeleri yayımlanmamıştır.

### Güvenli değerlendirme yaklaşımı

- Deneyleri yalnızca internetten ve üretim ağlarından yalıtılmış, sahibine ait sanal makinelerde yürütün.
- Laboratuvar trafiği için sentetik veri kullanın; gerçek kullanıcıların paketlerini veya kimlik bilgilerini toplamayın.
- ARP komşu tablosu ve DNS yapılandırmasında beklenmeyen değişiklikleri kayıtlı, yetkili temel durumla karşılaştırın.
- IP forwarding ayarını yalnızca okuyarak inceleyin; bu depodaki tanılama komutları sistem ayarını değiştirmez.
- Savunmada ağ segmentasyonu, uygun anahtarlarda DHCP snooping / Dynamic ARP Inspection, güvenilir DNS yapılandırması ve TLS/HTTPS doğrulamasını değerlendirin.
- Şüpheli bulguları ağ sahibine veya yetkili olay müdahale ekibine iletin.

Bu proje bir istismar kılavuzu değil; ARP/DNS risklerini tanıma ve azaltma üzerine eğitim notudur. Herhangi bir ağda test için önceden açık izin ve yazılı kapsam gerekir.
