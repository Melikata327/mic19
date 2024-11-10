# mic19
## آزمایش شماره سه : کنترل روشنایی با استفاده از فتوسل 

### هدف

در این آزمایش می خواهیم با استفاده از سنسور <strong>فتوسل</strong> در شرایط نوری متفاوت، روشنایی یک LED را تغییر دهیم.

---

### ابزار و وسایل
بردبورد	یک عدد
2	-برد آردوینو UNO	یک عدد
3-	سیم جامپر	هفت عدد
4	-کابل USB	یک عدد
5	-سنسور فتوسل	یک عدد
6-	مقاومت 220 اهمی	یک عدد
7	-مقاومت 1 کیلو اهمی	یک عدد
8	-دیود نوری	یک عدد

---

### توضیحات کلی 

سنسور فتوسل ( Photocell ) نوعی مقاومت نوری است یعنی از نیمه رساناهایی ساخته شده است که با تغییر شدت نور محیط مقدار مقاومت آن تغییر می کند به طوری که هر چه شدت نور بیشتر شود مقاومت فتوسل کاهش می یابد و بلعکس.  
بنابراین ما یک ولتاژ High به سمت یک ورودی آنالوگ از آردوینو می فرستیم و در مسیر آن یک سنسور فتوسل نیز قرار می دهیم. هر چه شدت نور محیط کمتر شود، میزان مقاومت سنسور بالاتر می رود بنابراین ولتاژ پایین تری به سمت ورودی آنالوگ خواهد فرستاد.

---

### سورس کد 
```cpp
int sensor;
int led = 10;

void setup() {
  Serial.begin(9600);
  pinMode(led, OUTPUT);
}

void loop() {
  sensor = analogRead(A3);
  Serial.print("Photocell Value = ");
  Serial.println(sensor);
  delay(100);

  if (sensor > 100) {
    digitalWrite(led, LOW);
    }

   else {
    digitalWrite(led, HIGH);
    }
}
```

---

### توصیف کد های برنامه 🧑🏻‍💻

در تابع setup یک سریال مانیتور با بیت ریت 9600 آغاز می کنیم و پین شماره 10 آردوینو را به عنوان خروجی برای LED تعیین می کنیم. در تابع loop مقدار دریافتی از ورودی آنالوگ A3 را می خوانیم که مقداری بین 0 تا 1023 می باشد. و سپس آن را در سریال مانیتور هر 100 میلی ثانیه یکبار چاپ می کنیم.  
در نهایت شرطی تعیین می کنیم که اگر مقدار دریافتی از A3 کمتر از 100 شد ( به معنی تاریک بودن محیط زیرا مقاومت افزایش داشته و جریان ورودی کاهش ) LED روشن شود در غیر این صورت همیشه خاموش بماند.

---
### توضیحات شماتیک مدار 

<ol>
<li>
اتصالات فتوسل
<ul>
<li>یک پایه به پین Vcc آردوینو</li>
<li>یک پایه به پین A3 آردوینو</li>
<li>پایه متصل شده به A3 همچنین متصل به پین Gnd آردوینو از طریق مقاومت 1 کیلو اهمی</li>
</ul>
</li>
<li>
اتصالات LED
<ul>
<li>پایه منفی به Gnd از طریق مقاومت 220 اهمی</li>
<li>پایه مثبت به پین 10 آردوینو</li>
</ul>
</li>
</ol>

---

### نتیجه گیری 

سنسور فتوسل می تواند در محیط های مختلفی مثل لامپ هایی با روشنایی اتوماتیک، گلخانه ها و... مفید باشد.
