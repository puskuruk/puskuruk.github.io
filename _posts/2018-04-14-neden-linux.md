Linux insanlar için zor görünen bir işletim sistemi olsa da terminalde rahat etmenizi sağlayacak kendim için yazdığım alias'ları paylaşmak ve bunları nasıl uygulayabileceğinizi anlatmak istiyorum.

Eski laptopım(Victor G3013)da olan ekranı kapatma fonksiyonu(fn+f2) gerçekten beni ok mutlu ediyordu ve kullanışlı olduğunu düşünüyordum bu nedenle linux sistemlerin esnekliğinden faydalanarak bunu terminalden aktif etmek için kullanığım bir alias yazdım.
```
#Bu alias ile terminalden kapat yazıp enter'a bastığınızda ekran tamamen kapanıyor ta ki mouse'u hareket ettirene kadar
#Kapat olarak tanımlamamın nedeni de ka yazıp tab'a bastığımda dire kapat'ın geliyor olması
alias kapat="xset -display :0.0 dpms force off"
```

Ruby ile öğrendiklerimi not alabileceğim bir uygulamamsı yazmıştım ve onu da programı çalıştırmak için uzun uzun ruby ...(uygulamanın adı) şeklinde yazmaktansa bir alias ile daha kolay erişişebilir bir hale getirdim.

```
#Tabiki de siz uygulamayı nereye kurduysanız orayı yazmalısınız
alias ne_ogrendim="ruby /home/puskuruk/WhatILearnedToday/whatdidulearned.rb"
```

Uygulama ise
```ruby
puts "What did you learned?"
whatdidulearned = gets
file = File.new("whatdidulearned.md", "a")
file.puts "\n"+Time.now.to_s+"\n"+whatdidulearned
```

Bu uygulama çalıştığında size "What did you learned?" diye soruyor ve sonrasında siz not almak istediğiniz şeyi yazdığınızda yazdığınız şeyi o anki saat ile "whatdidulearned.md" dosyasına yazıyor.

Not aldığım şeylere bakmak için ise şu alias'ı yazdım.

```
alias ogrendiklerim="vim /home/puskuruk/WhatILearnedToday/whatdidulearned.md"
```

Her gün düzenli olara girdiğim iki komut olan "sudo apt-get update" ve "sudo apt-get upgrade" komutlarını ise şu şekilde bir alias ile erişilmesi daha kolay hale getirdim.

```
alias yukselt="sudo apt-get update ; sudo apt-get upgrade"
```

##Bunları nasıl terminalime ekleyebilirim?
Bu komutları terminalinize eklemek için şu adımşları izlemelisiniz:

1-) Terminalinizi açıp kullandığınız metin editörü ile kullandığınız terminal kabuğu konfigurasyon dosyasını açın

örneğin:

```
#Vim ile zsh kabuğuna erişmek için
$ vim .zshrc
```
veya

```
#Vim ile bash(bourne again shell) kabuğuna erişmek için
```
$ vim .bashrc
```
2-) Boş bulduğunuz bir yere kullanmak istediğiniz komutu yapıştırın.


Linux işletim sistemi öğrendikçe/kullandıkça ne kadar pratik olduğunu fark edebileceğiniz sihirli bir arkadaş gibi.
