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
