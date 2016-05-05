# Προσωπικές Ρυθμίσεις-Εγκατάσταση του Arch Linux

Για την εγκατάσταση, ακολουθήστε το εγχειρίδιο που προτείνεται από το [Arch Linux] (https://wiki.archlinux.org/index.php/beginners'_guide).
Έχω γράψει έναν [προσωπικό οδηγό εγκατάστασης] (http://eiosifidis.blogspot.gr/2013/09/arch-linux-2013-09-01.html) που όμως είναι απαρχαιωμένος (πολλά έχουν αλλάξει από τότε). Θα επιχειρήσω να συγκεντρώσω εδώ όλες τις αλλαγές. Η συγγραφή του παρόντως είναι αποκλειστικά για να εγκαθιστώ όσο πιο γρήγορα γίνεται το Arch Linux. Αν το βρείτε χρηστικό και για εσάς, μπορείτε να το χρησιμοποιήσετε.

Οι οδηγίες αποτελούνται από τα εξής:

1. Τρόποι εγκατάστασης.
2. Βασική εγκατάσταση και γραφικό περιβάλλον.
3. Βασικά προγράμματα.
4. Ρυθμίσεις.

# 1. Τρόποι εγκατάστασης

* Ο παραδοσιακός τρόπος εγκατάστασης είναι μέσω τερματικού. Αρχικά κατεβάστε την [τελευταία έκδοση του ISO] (https://www.archlinux.org/download/) και εγγράψτε την σε ένα δισκάκι ή σε ένα USB. Αφού εκκινήσετε τον υπολογιστή σας, τότε προχωρήστε στο βήμα 2.

* Εάν είστε τύπος που δεν σας αρέσει το τερματικό και θέλετε την ευκολία σας, υπάρχουν αρκετές διανομές βασισμένες στο Arch που μπορείτε να χρησιμοποιήσετε. Δυο από τις καλύτερες θεωρώ τις [Antergos] (http://eiosifidis.blogspot.gr/2014/02/antergos-install.html) και την [Manjaro] (https://manjaro.github.io).

* Ένας εναλλακτικός τρόπος είναι με το σκριπτάκι AUI που όμως έχει σταματήσει την ανάπτυξη (δεν το συνιστώ). Αφού εκκινήσετε με το ISO που κατεβάσατε πριν, μπορείτε να χρησιμοποιήσετε το [σκριπτάκι αυτό] (https://github.com/helmuthdu/aui).

```
git://github.com/helmuthdu/aui

FIFO [system base]: cd <dir> && ./fifo
LILO [the rest...]: cd <dir> && ./lilo
```

* Εναλλακτικά, υπάρχουν οι επιλογές εγκατάστασης με text μορφή, βήμα προς βήμα. Από τις επιλογές που υπάρχουν, προτείνω με σειρά προτεραιότητας τις [Arch Anywhere] (http://arch-anywhere.org/)-> Δείτε το [βίντεο εγκατάστασης] (https://www.youtube.com/watch?v=3kV095iMO_k) στο οποίο στο τέλος, επιλέξτε να μπείτε με chroot στο εγκατεστημένο σύστημα και με την εντολή yaourt, εγκαθιστά και το AUR, [Feliz Linux] (https://sourceforge.net/projects/feliz/)-> Δείτε το [βίντεο εγκατάστασης] (https://www.youtube.com/watch?v=1vAjlz2pKb0) και το [Architect] (https://sourceforge.net/projects/architect-linux/)-> Δείτε το [βίντεο εγκατάστασης] (https://www.youtube.com/watch?v=sWR4qWsudwg). Σε όλες αυτές τις επιλογές, κατεβάζετε το ISO και αφού εκκινήσετε τον υπολογιστή σας, απαντάτε μια μια τις ερωτήσεις που σας θέτει.

* Εγκατάσταση Arch Linux με την χρήση liveDVD άλλης διανομής (με χρήση του bootstrap). Αυτό θα το περιγράψω λίγο περισσότερο γιατί ίσως να το χρησιμοποιώ πιο συχνά. Βασίζεται στο [wiki] (https://wiki.archlinux.org/index.php/Install_from_existing_Linux).

1.-> Κατεβάστε το [Bootstrap] (https://www.archlinux.org/download) (τσεκάρετε την έκδοση του αρχείου που κυκλοφορεί).

```
curl -O http://ftp.cc.uoc.gr/mirrors/linux/archlinux/iso/2016.05.01/archlinux-bootstrap-2016.05.01-x86_64.tar.gz
```

2.-> Αποσυμπιέστε το αρχείο:

```
tar xzf archlinux-bootstrap-2015.05.01-x86_64.tar.gz -C /tmp

cd /tmp
```

3-> Ξεκινήστε επιλέγοντας τους servers (χώρα προέλευσης):

```
nano /tmp/root.x86_64/etc/pacman.d/mirrorlist
```

Με ctrl+k σβήνετε όλη η γραμμή και με ctrl+x αποθηκεύετε τις αλλαγές.

ΣΗΜΕΙΩΣΗ: Εάν εγκαθιστάτε ένα σύστημα i686 από x86_64, πρέπει να επεξεργαστείτε και το αρχείο /tmp/root.i686/etc/pacman.conf όπου πρέπει να ορίσετε το Architecture = i686 ώστε ο pacman να φέρνει τα κατάλληλα πακέτα για i686.

4-> Λίγο πριν μπείτε ως chroot, χρειάζεται να δώστε τις εντολές.

Εάν έχετε εγκατεστημένη την έκδοση bash 4 ή νεότερη (δώστε στο τερματικό την εντολή: echo $BASH_VERSION), θα χρειαστεί να δώστε στο τερματικό την εντολή:

```
/tmp/root.x86_64/bin/arch-chroot /tmp/root.x86_64/
```

Αλλιώς, δώστε τα παρακάτω:

```
cd /tmp/root.x86_64
cp /etc/resolv.conf etc
mount -t proc /proc proc
mount --rbind /sys sys
mount --rbind /dev dev
mount --rbind /run run
(πρέπει να έχετε τον κατάλογο /run στο σύστημά σας)
chroot /tmp/root.x86_64 /bin/bash
```

5-> Αρχικοποίηση των κλειδιών:

```
pacman-key --init
pacman-key --populate archlinux
```

Στην συνέχεια ακολουθήστε τον οδηγό όπως περιγράφεται παρακάτω (με τα partitions κλπ).

# 2. Βασική εγκατάσταση και γραφικό περιβάλλον.

1.-> Κατατμήσεις
Τώρα, πρέπει να κάνετε τα partition. Με την εντολή cfdisk κάνουμε partions στον δίσκο όπου θα εγκαταστήσουμε το Arch. Αφού δημιουργήσουμε τα partitions, θέτουμε ως boot το partition όπου περιέχεται ο φάκελος /boot (συνήθως στο / εκτός και εάν έχουμε δημιουργήσει διαφορετική κατάτμηση γι'αυτό το λόγο, κάτι που γινόταν παλιά και συστήνεται από πολλούς).
Εάν δεν καταλαβαίνετε τι πρέπει να κάνετε, μπορείτε να πάρετε ένα δισκάκι με διανομή με γραφικό περιβάλλον, να ανοίξετε το gparted και να κάνετε τις κατατμήσεις στον δίσκο σας (εάν είναι καινούργιος). Προτείνεται, 20GB για το /, διπλάσια της φυσικής μνήμης ως swap (αν έχετε 4GB τότε χρησιμοποιήστε 1-2GB) και το υπόλοιπο ως /home. 

Kάνουμε format σε ext4,swap και μετά mount.

```
mkfs.ext4 /dev/sda1 (είναι το /)
mkswap /dev/sda2
mkfs.ext4 /dev/sda3 (είναι το /home)

mount /dev/sda1 /mnt
swapon /dev/sda2
mkdir /mnt/home && mount /dev/sda3 /mnt/home
```

Αν υποθέσουμε ότι δεν θέλετε να κάνετε format το /home σας (ή αν έχετε έναν άλλο δίσκο) και έστω ότι είναι το /dev/sda3, τότε ΠΑΡΑΛΕΙΠΕΤΕ την εντολή `mkfs.ext4 /dev/sda3`. Επίσης να έχετε υπόψιν σας ότι πρέπει να χρησιμοποιήσετε τον ίδιο χρήστη και συνθηματικό (θα δείτε παρακάτω πως δημιουργείται). Επίσης ΠΟΛΥ προσοχή εάν έχετε και 2ο δίσκο και τον αναγνωρίζει πχ ως sda1 και εκεί που θέλετε να εγκαταστήσετε το λειτουργικό, τον αναγνωρίζει ως sdb1, sdb2, sdb3. Σε αυτή την περίπτωση αλλάζουν οι παραπάνω εντολές καθώς επίσης και το "γράμμα" που θα δώσετε παρακάτω στην εγκατάσταση του Grub.

2.-> Επιλογή mirrorlist
Επιλέγουμε μόνο τα δικά μας mirrors μπαίνοντας στο αρχείο mirrorlist και διαγράφοντας τα υπόλοιπα (γρήγορη διαγραφή ολόκληρης σειράς με Ctrl+K).

```
nano /etc/pacman.d/mirrorlist
```

Σε περίπτωση που θέλουμε να διατηρήσουμε και τα ξένα, μπορούμε να βρούμε το πιο γρήγορο.

Κάντε μια ενημέρωση με την

```
pacman -Sy
```

Μετά εγκαταστήστε το reflector.

```
pacman -S reflector
```

Και δώστε την παρακάτω εντολή ώστε να αποθηκευτεί η σειρά με τα πιο γρήγορα mirrors.

```
reflector --verbose -l 200 -p http --sort rate --save /etc/pacman.d/mirrorlist
```

3.-> Εγκατασταση βασικού συστήματος.

```
pacstrap /mnt base base-devel
```

4.-> Εγκατάσταση του Grub2 bootloader (εγκαταστήστε και το wpa_supplicant που θα χρειαστεί πολύ αργότερα).

```
arch-chroot /mnt pacman -S grub-bios dialog wpa_supplicant
```

5.-> Δημιουργία του fstab.

```
genfstab -U -p /mnt >> /mnt/etc/fstab
```

6.-> Μπείτε ως chroot.

```
arch-chroot /mnt
```

7.-> Μέσα στο hostname γράφουμε το όνομα που θέλουμε να έχει ο υπολογιστής μας.

```
nano /etc/hostname
```

ή πιο απλά δώστε στο τερματικό την εντολή:

```
echo "mypc" > /etc/hostname
```

8.-> Καθορίζουμε το timezone.

```
ln -s /usr/share/zoneinfo/Europe/Athens /etc/localtime
```

9.-> Εδώ αν το σύστημα θέλουμε να ειναι GR διάγραφουμε το # μπροστά απο το el_GR.UTF-8. Προτιμήστε και την en_US.UTF-8.

```
nano /etc/locale.gen
```

ή πιο απλά δώστε στο τερματικό την εντολή:

```
echo -e "en_US.UTF-8 UTF-8\nel_GR.UTF-8 UTF-8" >> /etc/locale.gen
```

10.-> Μέσα στον παρακάτω προορισμό γράφουμε τη γλώσσα που επιλέξαμε και το localtime.

```
nano /etc/locale.conf
```

Καλό είναι το τερματικό του συστήματος να είναι στα Αγγλικά:

```
LANG="en_US.UTF-8"
LC_COLLATE="C"
LC_TIME="el_GR.UTF-8"
```

ή πιο απλά δώστε στο τερματικό την εντολή:

```
echo -e 'LANG="en_US.UTF-8"\nLC_MESSAGES="C"\nLC_TIME="el_GR.UTF-8"' >> /etc/locale.conf
```

11.-> Εφαρμόζουμε το locale.

```
locale-gen
```

12.-> Ρυθμίζουμε τον πυρήνα.

```
mkinitcpio -p linux
```

13.-> Ρυθμίζουμε το Grub bootloader.

```
grub-mkconfig -o /boot/grub/grub.cfg
grub-install --recheck /dev/sda
```

ΣΗΜΕΙΩΣΗ: Προσοχή εδώ. Όπως αναφέραμε παραπάνω, σε περίπτωση 2 δίσκων όπου πρέπει να εγκατασταθεί ο Grub στον sdb, θα πρέπει να αλλάξετε την 2η εντολή.

Τέλος για UEFI μπορείτε να ρίξετε μια ματιά στο [wiki] (https://wiki.archlinux.org/index.php/UEFI_Bootloaders).

14.-> Αλλάζουμε το συνθηματικό του root.

```
passwd root
```

Σε όλους τους οδηγούς εγκατάστασης προτείνουν να κάνετε επανεκκίνηση στο σημείο αυτό. Θεωρητκά μπορείτε να συνεχίσετε με την πλήρη εγκατάσταση και να κάνετε στο τέλος μια ολοκληρωτική επανεκκίνηση.

15.-> Multilib

Εάν έχετε εγκαταστήσει 64bit σύστημα και θέλετε να εγκαταστήσετε εφαρμογές 32bit, πρέπει να κάνετε uncomment (σβήστε το σημαδάκι #). Για περισσότερες πληροφορίες, δείτε το [wiki] (https://wiki.archlinux.org/index.php/Multilib).

Ανοίξτε το αρχείο:

```
nano /etc/pacman.conf
```

και σβήστε το # από το αποθετήριο:

```
[multilib]
Include = /etc/pacman.d/mirrorlist
```

Κάντε μια ανανέωση των πηγών με την εντολή:

```
pacman -Syy
```

16.->  Ενεργοποίηση AUR.

Το AUR είναι το αποθετήριο της κοινότητας. Εκεί θα βρείτε τα πάντα. Εάν δεν έχετε κάνει επανεκκίνηση και να εισέλθετε με γραφικό περιβάλλον χρήστη, τότε δεν θα μπορείτε να το χρησιμοποιήσετε. Όμως ας το εγκαταστήσετε από τώρα για να μην το ξεχάσετε μετά.

Επεξεργαστείτε το αρχείο:
```
nano /etc/pacman.conf
```

Και προσθέστε στο τέλος την διεύθυνση:
```
[archlinuxfr]
SigLevel = Optional TrustAll
Server = http://repo.archlinux.fr/$arch 
```

Εγκαταστήστε το yaourt με την εντολή:
```
pacman -Sy yaourt fakeroot
```

Αφού εγκατασταθεί ο yaourt καλό θα ήταν να αφαιρέσουμε τις γραμμές που μόλις προσθέσαμε από το αρχείο `/etc/pacman.conf`.

17.-> Προσθήκη Χρήστη.

```
useradd -m -g users -G wheel,audio,video,optical,storage,lp,network,uucp -s /bin/bash diamond
```

Και αλλάξτε τον κωδικό του.
```
passwd diamond 
```

Εφόσον παρακάτω θα εγκαταστήσετε το sudo για να το χρησιμοποιήσετε, θα μπείτε στην ομάδα wheel (παραπάνω που δημιουργήσαμε τον χρήστη), πρέπει να ανοίξετε το αρχείο /etc/sudoers (`nano /etc/sudoers`) και να σβήσετε το # μπροστά από το

```
## Uncomment to allow members of group wheel to execute any command
%wheel ALL=(ALL) ALL
```

18.-> Εγκατάσταση γραφικών-κάρτας γραφικών.

X install
```
pacman -S xorg xorg-server xorg-server-utils xorg-apps xorg-xinit xorg-twm xorg-xclock xterm
```

για 3d
```
pacman -S mesa
```

για γενικούς οδηγούς (προαιρετικό)
```
pacman -S xf86-video-vesa
```

Τώρα είναι η ώρα να εγκαταστήσετε τους drivers της κάρτας γραφικών σας. Περισσότερες πληροφορίες δείτε στην ιστοσελίδα του wiki.

Για κάρτες Nvidia

Εγκαταστήστε τον ανοικτό driver
```
pacman -S xf86-video-nouveau
```

Εγκαταστήστε τον κλειστό driver
```
pacman -S nvidia
```

Σημείωση: Για παλιές κάρτες υπάρχουν τα πακέτα nvidia-71xx και το nvidia-96xx. Ρυθμίστε την κάρτα με το nvidia-xconfig. Όταν εγκαθιστάτε τον xorg, γίνεται αυτόματα εγκατάσταση ο nouveau (οπότε δεν χρειάζεται να δώσετε την παραπάνω εντολή). Ο κλειστός driver της NVIDIA είναι στα επίσημα repo. Εάν βάλετε τον κλειστό driver της Nvidia, δεν χρειάζεται να εγκαταστήσετε τον mesa. Σε περίπτωση που εγκαταστήσατε τον ανοικτό οδηγό και θέλετε να τον αλλάξετε στον κλειστό, απεγκαταστήστε τον xf86-video-nouveau (pacman -Rs xf86-video-nouveau xf86-video-intel xf86-video-ati) και μετά εγκαταστήστε τον κλειστό. Στην προηγούμενη εντολή απεγκαθιστούμε και οποιονδήποτε άλλον driver που χρησιμοποιεί mesa, διότι ο nvidia εγκαθιστά δικιά του έκδοση.

Για κάρτες ΑΤΙ

Εγκαταστήστε τον ανοικτό driver
```
pacman -S xf86-video-ati
```

Εγκαταστήστε τον κλειστό driver
```
yaourt -S catalyst-dkms
```

Ο κλειστός οδηγός της ATI βρίσκεται στο AUR (αυτό μπορείτε να το εγκαταστήσετε αμέσως μόλις μπείτε ως χρήστης, αφού τον έχετε προσθέσει παραπάνω).

Για κάρτες Intel

Εγκαταστήστε τον ανοικτό driver
```
pacman -S xf86-video-intel
```

# 

Σημείωση: Το πακέτο xf86-video-intel είναι για chipsets i810/i830/i9xx για το 740 υπάρχει το xf86-video-i740.

19.-> Εγκατάσταση ήχου και codecs.

```
pacman -S alsa-utils alsa-oss pulseaudio pulseaudio-alsa gstreamer0.10-plugins gstreamer0.10-ffmpeg ffmpeg flashplugin
```

20.-> Εγκατάσταση ποντικιού κλπ.

```
pacman -S xf86-input-synaptics xf86-input-mouse xf86-input-keyboard xf86-input-evdev
```

21.-> Εγκατάσταση desktop. Εγώ προτιμώ το GNOME.

```
pacman -S gdm gnome gnome-extra
```

Ενεργοποιήστε το GDM να ξεκινάει αυτόματα.
```
systemctl enable gdm.service 
```

22.-> Εγκατάσταση headers.

```
pacman -S linux-headers
```

23.-> Επανεκκίνηση

Βγαίνουμε από το chroot.
```
exit
```

Κάνουμε unmount και reboot.
```
umount /mnt/{home,}
reboot 
```

# 3. Εγκατάσταση βασικών προγραμμάτων.

1.-> Εγκατάσταση [LibreOffice] (https://wiki.archlinux.org/index.php/LibreOffice).

```
pacman -S libreoffice-still libreoffice-still-sdk libreoffice-still-el jdk7-openjdk jre7-openjdk
```

Σε περίπτωση που θέλετε τη νεότερη έκδοση, μπορείτε να εκγαταστήσετε τα

```
pacman -S libreoffice-fresh libreoffice-fresh-sdk libreoffice-fresh-el jdk7-openjdk jre7-openjdk 
```

2.-> Εγκατάσταση διαφόρων προγραμμάτων που χρησιμοποιώ προσωπικά. Σβήστε ότι δεν χρειάζεστε.

```
pacman -S sudo v4l-utils x264 cups transmission-gtk subdownloader subtitleeditor gnome-subtitles audacity audacious audacious-plugins smplayer smtube mplayer asunder dvdrip openshot devede winff mencoder sound-juicer youtube-dl easytag inkscape gimp gutenprint gphoto2 f-spot numlockx mc davfs2 aria2 hexchat polari pidgin chromium filezilla firefox firefox-i18n-el thunderbird thunderbird-i18n-el sox subversion git meld gtranslator unzip acpid htop glances lsof powertop testdisk deja-dup libdvdcss libdvdnav libdvdread libdca timidity++ ogmtools mcomix evince xchm gparted stardict gnome-settings-daemon telepathy-gabble gnome-common alacarte seahorse virtualbox vde2 virtualbox-host-dkms net-tools gnome-music gnome-photos bchunk gst-libav skype pdfsam gnome-boxes pkgfile gconf-editor hplip aspell-el
```

3.-> Προγράμματα από το AUR.
```
yaourt -S viber teamviewer10 dropbox nautilus-dropbox google-talkplugin google-musicmanager menulibre pdfcrack pdfshuffler luckybackup rabbitvcs rabbitvcs-nautilus chromium-pepper-flash google-chrome imagewriter cdw simpleburn multisystem virtualbox-ext-oracle ubuntu-themes humanity-icon-theme simplescreenrecorder os-prober unetbootin libreoffice-extension-languagetool yandex-disk pcloud hplip-plugin --noconfirm
```

Το --noconfirm το χρησιμοποιείτε για να μην σας ρωτάει συνέχεια.

Στον messanger του facebook, θα σας κάνει μια ερώτηση και απαντάτε ναι στην αντικατάσταση αρχείων.

```
yaourt -S messengerfordesktop
```


Όταν τελειώσει η εγκατάσταση των παραπάνω, όσον αφορά το teamviewer, πρέπει να δώσετε τις εντολές:
```
systemctl enable teamviewerd
```

Για να μην εκκινεί κάθε φορά η υπηρεσία, εγώ έχω εισάγει στο .bashrc το alias για να το ξεκινώ κάθε φορά που το χρειάζομαι (θα σας αναφέρω παρακάτω και το bashrc). Η εντολή είναι η:
```
sudo systemctl start teamviewerd
```

Όσον αφορά το Virtual Box, πρέπει να βάλετε τον χρήστη στην ομάδα vboxusers (δείτε περισσότερες πληροφορίες στο [wiki] (https://wiki.archlinux.org/index.php/VirtualBox) ):
```
gpasswd -a yourusername vboxusers 
```
