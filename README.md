# BSA
Basic Static Analysis


																		TryHackMe - Basic Static Analysis 
																		=================================

Task 3  String search
=====================

On the Desktop in the attached VM, there is a directory named 'mal' with malware samples 1 to 6. Use floss to identify obfuscated strings found in the samples named 2, 5, and 6. Which of these samples contains the string 'DbgView.exe'?

FLARE VM-ə daxil olan bir neçə digər alətlər sətir axtarışı üçün istifadə edilə bilər. Məsələn, CyberChef (Desktop>FLARE>Utilities>Cyberchef) əsas sətir axtarışı üçün də reseptə malikdir. PEstudio (Desktop>FLARE>Utilities>pestudio) həmçinin sətirli axtarış yardım proqramını təmin edir. PEstudio həmçinin sətirlər haqqında əlavə məlumat verir, məsələn, kodlaşdırma, sətir ölçüsü, sətir tapıldığı binar sistemdə ofset və sətirin nə ilə əlaqəli olduğunu təxmin etmək üçün göstəriş. O, həmçinin bəzi imzalara qarşı sətirlərə uyğun gələn qara siyahı üçün sütuna malikdir.

pestudio acdigdan sonra asagdaki comandi yazirig

C:\Users\Administrator>cd Desktop

FLARE Fri 12/22/2023  3:29:17.91
C:\Users\Administrator\Desktop>floss --no-static-strings mal\2

FLOSS decoded 0 strings

FLOSS extracted 0 stackstrings

Finished execution after 0.016000 seconds

FLARE Fri 12/22/2023  3:29:24.67
C:\Users\Administrator\Desktop>floss --no-static-strings mal\5

FLOSS decoded 0 strings

FLOSS extracted 0 stackstrings

Finished execution after 0.015000 seconds

FLARE Fri 12/22/2023  3:29:39.25
C:\Users\Administrator\Desktop>floss --no-static-strings mal\6
WARNING:envi.codeflow:parseOpcode error at 0x1400596c8 (addCodeFlow(0x140058558)): InvalidInstruction("'c5eeffff440fb70233c041baffff0000' at 0x1400596c8L",)
WARNING:envi.codeflow:parseOpcode error at 0x14004edc2 (addCodeFlow(0x14004b0d4)): InvalidInstruction("'db75178b1509f30400488d0d2ca50300' at 0x14004edc2L",)
WARNING:envi.codeflow:parseOpcode error at 0x14004e645 (addCodeFlow(0x14004e5b0)): InvalidInstruction("'db75178b1586fa0400488d0df9ab0300' at 0x14004e645L",)

FLOSS decoded 1 strings
@@AD

FLOSS extracted 45 stackstrings
Dbgview.exe
Dbgview.exe
AVQZAWI
Dbgview.exe
Dbgview.exe
Dbgview.exe
Dbgview.exe
Dbgview.exe
Dbgview.exe
Dbgview.exe
Dbgview.exe
D$ H
Dbgview.exe
Dbgview.exe
L$ H
Dbgview.exe
Dbgview.exe
Dbgview.exe
Dbgview.exe
Dbgview.exe
Dbgview.exe
Dbgview.exe
A_A^
Dbgview.exe
Dbgview.exe
Dbgview.exe
Dbgview.exe
Dbgview.exe
Dbgview.exe
Dbgview.exe
112222I
Dbgview.exe
Dbgview.exe
Dbgview.exe
Dbgview.exe
Dbgview.exe
Dbgview.exe
Dbgview.exe
D$ H
@@AD
Dbgview.exe
Dbgview.exe
Dbgview.exe
Dbgview.exe
Dbgview.exe

Finished execution after 69.979000 seconds

FLARE Fri 12/22/2023  3:31:18.92
Answer: 6



Task 4  Fingerprinting malware
==============================

In the samples located at Desktop\mal\ directory in the attached VM, which of the samples has the same imphash as file 3?

Fayl hashlərinin hesablanması üçün ümumi istifadə olunan üsullar:
Faylların identifikasiyası üçün tam faylın hashı alınır. Hash götürməyin müxtəlif üsulları var. Ən çox istifadə edilən üsullar bunlardır:

Mən Md5
Şa1sum
Şa256sum
İlk iki növ heş indi etibarsız hesab edilir və ya toqquşma hücumlarına meyllidir (iki və ya daha çox giriş eyni hash ilə nəticələndikdə). Bu hash funksiyaları üçün toqquşma hücumu çox ehtimal olmasa da, hələ də mümkündür. Buna görə də, sha256sum hazırda fayl hashını hesablamaq üçün ən təhlükəsiz üsul hesab olunur. Əlavə edilmiş VM-də biz görə bilərik ki, bir çox utilitlər bizim üçün fayl heşlərini hesablayır.

Heshlərdən istifadə edərək oxşar faylları tapmaq:
Hash funksiyalarının zərərli proqram analitikinə kömək etdiyi başqa bir ssenari, hashlərdən istifadə edərək oxşar faylları müəyyən etməkdir. Biz artıq müəyyən etdik ki, faylın məzmununda cüzi dəyişiklik belə fərqli hash ilə nəticələnəcək. Bununla belə, bəzi hash növləri müxtəlif fayllar arasında oxşarlığı müəyyən etməyə kömək edə bilər. Gəlin bunlardan bəziləri haqqında öyrənək.

Imphash:
Imphash "hash idxalı" deməkdir. İdxal icra edilə bilən faylın digər fayllardan və ya Dinamik Əlaqəli Kitabxanalardan (DLL) idxal etdiyi funksiyalardır. İmphash, zərərli proqram nümunəsinin idxal etdiyi funksiya çağırışlarının/kitabxanalarının hashıdır və bu kitabxanaların nümunədə mövcud olma sırasıdır. Bu, eyni təhlükə qruplarından nümunələri müəyyən etməyə və ya oxşar fəaliyyətləri yerinə yetirməyə kömək edir. Imphash haqqında ətraflı məlumatı Mandiantın bloqunda burada tapa bilərsiniz.

Nümunənin İmphaşını hesablamaq üçün PEstudio-dan istifadə edə bilərik. 

https://www.mandiant.com/resources/blog/tracking-malware-import-hashing
https://bazaar.abuse.ch/browse.php?search=imphash%3A756fdea446bc618b4804509775306c0d


IMPHASH 1 
imphash,F397831B8900AFF7FBEF2FFDE97C2603

IMPHASH 2
imphash,FDF028EC701B2D6858C7AD4B1EC13C1E

IMPHASH 3
imphash,F397831B8900AFF7FBEF2FFDE97C2603

IMPHASH 4
imphash,n/a

IMPHASH 5
imphash,2916DDA3C80B39A540B60C072A91A915

IMPHASH 6
imphash,7997426B781E320BCC031754360DF27F
Answer: 1



Using the ssdeep utility, what is the percentage match of the above-mentioned files?

C:\Users\Administrator\Desktop>ssdeep-2.14.1\ssdeep.exe mal\*
ssdeep,1.1--blocksize:hash:hash,filename
3072:C3twbyJdvGwRCf/swDQheOAmN4hMRl37G:8EacOAmN6C,"C:\Users\Administrator\Desktop\mal\1"
768:fMjB/JpMfHDWqpuXDvod3UmQmv4acY2GS2C9xjwhU:UFQlpSDvoJrbvUfGS2q,"C:\Users\Administrator\Desktop\mal\2"
1536:C3tvICAqw8IKVn2wJk0c8PoYJvGwRCwAL6pILgl7vBIQtCnDkbZ3eOAmV2u4hnnM:C3twbyJdvGwRCf/swDQheOAmN4hM,"C:\Users\Administrator\Desktop\mal\3"
24576:u7DtlSDAlZvEFZhbS7buPPcedeHP5XLnkO3hGL8Siw9zVZprY8fWg5r11O:8OKVizL3cvtkO3hmVVZBYu5r1M,"C:\Users\Administrator\Desktop\mal\4"
12288:z+IIs67xrXWxgxMdplNGvIcGZwwDVHJXuDzKYzIE5P/XiS6lYSz8uahDtbNL6WTW:z+PsGlsFGgcQDJJQ,"C:\Users\Administrator\Desktop\mal\5"
24576:UCsTPcqE9S7tdODN+6ybJVCy2pvZHGOzPBjRj4AFsb:UCO7tsp+6ybJVChpRjvs,"C:\Users\Administrator\Desktop\mal\6"

FLARE Fri 12/22/2023  3:47:09.81
C:\Users\Administrator\Desktop>ssdeep-2.14.1\ssdeep.exe mal

FLARE Fri 12/22/2023  3:47:48.18
C:\Users\Administrator\Desktop>ssdeep-2.14.1\ssdeep.exe mal/
C:\Users\Administrator\Desktop\mal\: Is a directory

FLARE Fri 12/22/2023  3:47:56.62
C:\Users\Administrator\Desktop>ssdeep-2.14.1\ssdeep.exe mal\
C:\Users\Administrator\Desktop\mal\: Is a directory

FLARE Fri 12/22/2023  3:47:59.40
C:\Users\Administrator\Desktop>ssdeep-2.14.1\ssdeep -l -r -d mal
mal\3 matches mal\1 (93)

FLARE Fri 12/22/2023  3:48:33.17
Answer: 93






Task 5  Signature-based detection
=================================


Yara rules 

https://github.com/Yara-Rules/rules

Yara qaydaları imza əsaslı qayda növüdür. Zərərli proqram tədqiqatçıları üçün məşhur olaraq nümunəyə uyğun İsveçrə ordusu bıçağı adlanır. Yara faylda olan onaltılıq və sətirlər kimi binar və mətn nümunələrinə əsaslanan məlumatları müəyyən edə bilər. TryHackMe-nin xüsusi otaq sizi maraqlandırırsa, Yara qaydaları üçün var.

Təhlükəsizlik icması ehtiyaclarımıza uyğun istifadə edə biləcəyimiz açıq mənbəli Yara qaydalarının anbarını dərc edir. Zərərli proqramı təhlil edərkən, cəmiyyətin kollektiv müdrikliyini öyrənmək üçün bu depodan istifadə edə bilərik. Bununla belə, bu qaydalardan istifadə edərkən bəzilərinin kontekstdən asılı ola biləcəyini unutmayın. Bəziləri də qeyri-zərərli ola biləcək nümunələri müəyyən etmək üçün istifadə edilə bilər. Beləliklə, bir qaydanın vurulması faylın zərərli olması demək deyil. Daha yaxşı başa düşmək üçün, lütfən, ən yaxşı şəkildə tətbiq oluna biləcəyi istifadə halını müəyyən etmək üçün xüsusi qaydanın sənədlərini oxuyun.


Capa:
Capa Mandiant tərəfindən yaradılmış başqa açıq mənbə alətidir. Bu alət PE faylında tapılan imkanları müəyyən etməyə kömək edir. Capa faylları oxuyur və idxal, sətir, mutexes və faylda mövcud olan digər artefaktlar kimi imzalar əsasında faylın davranışını müəyyən etməyə çalışır. Capa haqqında ətraflı məlumat üçün onun Github səhifəsinə və ya Mandiant'ın bloq yazısına baş çəkə bilərik. Capa təqdim edir.
https://github.com/mandiant/capa

C:\Users\Administrator>cd Desktop

FLARE Fri 12/22/2023  4:45:06.41
C:\Users\Administrator\Desktop>capa -h
usage: capa.exe [-h] [--version] [-v] [-vv] [-d] [-q] [--color {auto,always,never}] [-f {auto,pe,sc32,sc64,freeze}] [-b {vivisect,smda}] [-r RULES] [-t TAG] [-j] sample

The FLARE team's open-source tool to identify capabilities in executable files.

İndi Desktop\mal\4 faylını təhlil etmək və aşağıdakı suallara cavab vermək üçün capa istifadə edək.

How many matches for anti-VM execution techniques were identified in the sample?
Answer: 86

Does the sample have to capability to suspend or resume a thread? Answer with Y for yes and N for no.
Answer: y

What MBC behavior is observed against the MBC Objective 'Anti-Static Analysis'?
Answer: Disassembler Evasion::Argument Obfuscation [B0012.001]

Malware Beharvior Catalog
https://github.com/MBCProject/mbc-markdown




At what address is the function that has the capability 'Check HTTP Status Code'?


Task 6  Leveraging the PE header
================================


Open the sample Desktop\mal\4 in PEstudio. Which library is blacklisted?
Pestudio >> open file >> mal\4 >> Libraries
Answer: rpcrt4.dll

What does this dll do?
Answer: Remote Procedure Call Runtime
