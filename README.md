## SchoolProjectDatabaseDesign
# Eğitim Projemdeki SQL Ödevim

----------------------------------------------------------------------------------------------------------------------------------

Projenin Diagram Alanı Üzerinden Genel Görüntüsü


![resim](https://github.com/AhmetSahinNL/SchoolProjectDatabaseDesign/assets/139613517/38f93cdc-ab84-460c-bd7a-79f3ce53b983)

 
----------------------------------------------------------------------------------------------------------------------------------

Bu tabloda kişilerin tüm temel bilgileri yer almaktadır.


![resim](https://github.com/AhmetSahinNL/SchoolProjectDatabaseDesign/assets/139613517/36fc7662-f58b-48c5-b9b1-fa5514f600cb)


• Status ==> Öğrenci, öğretmen veya farklı bir birimde olan kişileri temsil eden alandır.
• IdentificationNumber ==> TC Kimlik numarasının yazıldığı alan.
• FirstName ==> İsim alanı.
• LastName ==> Soyisim alanı.
• Gender ==> Cinsiyet alanı.
• DateOfBirth ==> Doğum tarihi alanı.
• ContactId ==> E-posta, telefon ve adres gibi diğer iletişim bilgilerinin çekildiği alandır. (Bilgiler  [ContactInformations] tablosundan çekilmektedir.

NOT = { Bu tablodaki 'Id' değeri ile 'Students' tablosundaki 'PersonId' ve 'Teachers' tablosundaki 'PersonId' değerlerine kişilere ait bilgileri aktarmaktadır. }


![resim](https://github.com/AhmetSahinNL/SchoolProjectDatabaseDesign/assets/139613517/e05179cc-68c0-46ae-b91a-cfa42e46055d)


```MYSQL
CREATE TABLE [dbo].[Persons](
	[Id] [int] IDENTITY(1,1) NOT NULL,
	[Status] [varchar](20) NOT NULL,
	[IdentificationNumber] [char](11) NOT NULL,
	[FirstName] [varchar](50) NOT NULL,
	[LastName] [varchar](50) NOT NULL,
	[Gender] [varchar](6) NOT NULL,
	[DateOfBirth] [datetime] NOT NULL,
	[ContactId] [int] NULL,
 CONSTRAINT [PK_Persons] PRIMARY KEY CLUSTERED 
(
	[Id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
```

----------------------------------------------------------------------------------------------------------------------------------


İletişim bilgilerinin depolandığı tablodur.


![resim](https://github.com/AhmetSahinNL/SchoolProjectDatabaseDesign/assets/139613517/d8351b7c-c51b-43b1-ab20-80a8c5ae8eda)


• PhoneNumber ==> Telefon numarası bilgilerini tutan alandır.
• Email ==> E posta adreslerinin bulunduğu kısım.
• Address ==> Adres bilgilerinin yer aldığı değerdir.

NOT = { Bu tablo 'Id' alanı üzerinden Persons tablosundaki 'ContactId' değerine bilgi aktarımı sağlamaktadır. }

```MYSQL
CREATE TABLE [dbo].[ContactInformations](
	[Id] [int] IDENTITY(1,1) NOT NULL,
	[PhoneNumber] [char](11) NULL,
	[Email] [varchar](100) NULL,
	[Address] [varchar](max) NULL,
 CONSTRAINT [PK_ContactInformations] PRIMARY KEY CLUSTERED 
(
	[Id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY] TEXTIMAGE_ON [PRIMARY]
```

----------------------------------------------------------------------------------------------------------------------------------


Öğrencilere ait bilgilerin bulunduğu tablodur.


![resim](https://github.com/AhmetSahinNL/SchoolProjectDatabaseDesign/assets/139613517/1aa5e268-984e-4880-ac42-99ed6f92b0ff)


• PersonId ==> Persons tablosundan öğrencilere ait temel bilgiler çekilmektedir.
• StudentId ==> Öğrenci numarasının bulunduğu kısım.
• IsActive ==> Öğrencinin aktif bir öğrenci ya da öğrenci ilişiğinin kesildiğini gösteren alandır.
• NOTE ==> Öğrencinin okul ile ilişkisi kesildi ise sebebinin açıklandığı kısımdır.

NOT = { Bu tablodaki 'StudentId' değeri 'Exams' tablosundaki 'StudentId' ve 'Attendances' tablosundaki 'StudentId' değerlerine öğrencilerin bilgilerini aktarmaktadır. }

```MYSQL
CREATE TABLE [dbo].[Students](
	[Id] [int] IDENTITY(1,1) NOT NULL,
	[PersonId] [int] NOT NULL,
	[StudentId] [varchar](4) NOT NULL,
	[IsActive] [bit] NOT NULL,
	[NOTE] [varchar](max) NULL,
 CONSTRAINT [PK_Students] PRIMARY KEY CLUSTERED 
(
	[StudentId] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY] TEXTIMAGE_ON [PRIMARY]
```

----------------------------------------------------------------------------------------------------------------------------------


Öğretmen bilgilerinin bulunduğu tablodur.


![resim](https://github.com/AhmetSahinNL/SchoolProjectDatabaseDesign/assets/139613517/aeb12ca4-22f0-4415-ba00-ea2674c50eb7)



• PersonId ==> Persons tablosundan öğretmenlere ait temel bilgiler çekilmektedir.
• TeacherId ==> Öğretmen numarasının bulunduğu kısım.
• Branch ==> Öğretmenin mesleki branşını açıklayan bölüm.
• StartingDate ==> İşe başlama tarihini belirtir.

NOT = { Bu tablodaki 'TeacherId' değeri 'Exams' tablosundaki 'ExamTeacherId' ve 'Attendances' tablosundaki 'TeacherId' değerlerine öğretmenlerin bilgilerini aktarmaktadır. }

```MYSQL
CREATE TABLE [dbo].[Teachers](
	[Id] [int] IDENTITY(1,1) NOT NULL,
	[PersonId] [int] NOT NULL,
	[TeacherId] [varchar](4) NOT NULL,
	[Branch] [varchar](50) NOT NULL,
	[StartingDate] [date] NOT NULL,
 CONSTRAINT [PK_Teachers] PRIMARY KEY CLUSTERED 
(
	[TeacherId] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
```
----------------------------------------------------------------------------------------------------------------------------------


Sınıf isimlerinin bulunduğu tablodur.


![resim](https://github.com/AhmetSahinNL/SchoolProjectDatabaseDesign/assets/139613517/8ae16c90-53ea-4ca7-9f86-f3d43ab8acce)



NOT = { Bu tablodaki 'Id' değeri 'Exams' tablosundaki 'ClassId' ve 'Attendances' tablosundaki 'ClassId' değerlerine sınıf bilgilerini aktarmaktadır. }

```MYSQL
CREATE TABLE [dbo].[Classes](
	[Id] [int] IDENTITY(1,1) NOT NULL,
	[ClassName] [varchar](50) NOT NULL,
 CONSTRAINT [PK_Classes] PRIMARY KEY CLUSTERED 
(
	[Id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
```

----------------------------------------------------------------------------------------------------------------------------------


Derslerin bulunduğu tablodur.


![resim](https://github.com/AhmetSahinNL/SchoolProjectDatabaseDesign/assets/139613517/2da57930-65b1-4c63-a086-e875be2bd911)



NOT = { Bu tablodaki 'Id' değeri 'Exams' tablosundaki 'LessonId' ve 'Attendances' tablosundaki 'LessonId' değerlerine ders bilgilerini aktarmaktadır. }

```MYSQL
CREATE TABLE [dbo].[Lessons](
	[Id] [int] IDENTITY(1,1) NOT NULL,
	[CourseName] [varchar](50) NOT NULL,
 CONSTRAINT [PK_Lessons] PRIMARY KEY CLUSTERED 
(
	[Id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
```

----------------------------------------------------------------------------------------------------------------------------------


Yoklama bilgilerinin tutulduğu tablodur.


![resim](https://github.com/AhmetSahinNL/SchoolProjectDatabaseDesign/assets/139613517/0d34daf5-9f54-4b22-80f0-adde3f369e8f)


• TeacherId ==> Öğretmen numarasının bulunduğu kısım.
• ClassId ==> Sınıf bilgilerinin bulunduğu alan. (Bilgiler [Classes] tablosundan çekilmektedir.)
• LessonId ==> Ders bilgilerinin bulunduğu kısım. (Bilgiler [LessonId] tablosundan çekilmektedir.)
• StudentId ==> Öğrenci numarasının bulunduğu alan. (Bilgiler [StudentId] tablosundan çekilmektedir.)
• Date ==> Yoklama alınan tarihi belirtir. 
• AttendanceStatus ==> Yoklamanın durumunu yani gelmeyen öğrencileri belirtir. Öğrenci gelmedi ise işlem 'False' döner.


![resim](https://github.com/AhmetSahinNL/SchoolProjectDatabaseDesign/assets/139613517/8bc39aa1-c038-4cd9-8ce5-54b5f797f81a)


```MYSQL
CREATE TABLE [dbo].[Attendances](
	[Id] [int] IDENTITY(1,1) NOT NULL,
	[TeacherId] [varchar](4) NOT NULL,
	[ClassId] [int] NOT NULL,
	[LessonId] [int] NOT NULL,
	[StudentId] [varchar](4) NOT NULL,
	[Date] [date] NOT NULL,
	[AttendanceStatus] [bit] NOT NULL,
 CONSTRAINT [PK_Attendances] PRIMARY KEY CLUSTERED 
(
	[Id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
```

----------------------------------------------------------------------------------------------------------------------------------


Sınavların ve sonuçlarının bulunduğu tablodur. 


![resim](https://github.com/AhmetSahinNL/SchoolProjectDatabaseDesign/assets/139613517/9881a9c3-7180-4616-9dc5-1124308eacef)


• StudentId ==> Sınava girecek öğrencinin numarasının bulunduğu alandır.
• ExamTeacherId ==> Sınav gözetmenliği yapan öğretmenin numarasının bulunduğu kısımdır.
• ClassId ==> Sınavın gerçekleşeceği sınıfı belirtir.
• LessonId ==> Hangi dersten sınav olunacağını belirtir.
• Exam1 ==> 1. Sınav sonucunun tutulduğu alan.
• Exam2 ==> 2. Sınav sonucunun tutulduğu alan.
• Average ==> 2 Sınav da tamamlandıktan sonra sınav ortalamalarının otomatik olarak hesaplandığı kısımdır.


![resim](https://github.com/AhmetSahinNL/SchoolProjectDatabaseDesign/assets/139613517/7a517c97-321b-4897-9bfd-2ca3add8783b)


```MYSQL
CREATE TABLE [dbo].[Exams](
	[Id] [int] IDENTITY(1,1) NOT NULL,
	[StudentId] [varchar](4) NOT NULL,
	[ExamTeacherId] [varchar](4) NOT NULL,
	[ClassId] [int] NOT NULL,
	[LessonId] [int] NOT NULL,
	[Exam1] [varchar](3) NOT NULL,
	[Exam2] [varchar](3) NOT NULL,
	[Average] [varchar](3) NULL,
 CONSTRAINT [PK_Exams] PRIMARY KEY CLUSTERED 
(
	[Id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
```
----------------------------------------------------------------------------------------------------------------------------------


************  PROSEDÜRLER ************


1-) Öğrenci numarasına göre belirli bir öğrencinin bilgilerini getiren prosedür.


```MYSQL
CREATE PROCEDURE [dbo].[GetStudentInfoByStudentId]
    @StudentId VARCHAR(4)
AS
BEGIN
    SELECT
        p.FirstName,
        p.LastName,
        p.Gender,
        p.DateOfBirth,
        s.StudentId,
        s.IsActive,
        s.NOTE
    FROM Students s
    JOIN Persons p ON s.PersonId = p.Id
    WHERE s.StudentId = @StudentId;
END;
```

Bu kod ile de öğrencinin bilgileri çekilebilir.

```MYSQL
EXEC GetStudentInfoByStudentId @StudentId = '1001';
```


2-) Öğrenci numarası ile belirli bir öğrencinin sınavlarını ve sınav ortalamasını getiren prosedürdür.


```MYSQL
ALTER PROCEDURE [dbo].[GetStudentExamResults]
    @StudentId VARCHAR(4)
AS
BEGIN
    SELECT
        e.Exam1,
        e.Exam2,
        e.Average
    FROM Exams e
    WHERE e.StudentId = @StudentId;
END;
```

Bu kod ile de sınav bilgileri çekilebilir.

```MYSQL
EXEC [dbo].[GetStudentExamResults] @StudentId = '1001';
```

3-) Belirlenen öğrenciye ait tüm kayıt bilgilerini silen prosedürdür.


```MYSQL
CREATE PROCEDURE [dbo].[DeleteStudent]
    @StudentId VARCHAR(4)
AS
BEGIN
    DECLARE @PersonId INT

    SELECT @PersonId = PersonId FROM Students WHERE StudentId = @StudentId

    DELETE FROM Students WHERE StudentId = @StudentId

    DELETE FROM Persons WHERE Id = @PersonId
END;
```

Bu kod ile de silinecek öğrencinin numarasını yazıp prosedürü kullanabiliriz.

```MYSQL
EXEC [dbo].[DeleteStudent]
    @StudentId = '1001';
```

----------------------------------------------------------------------------------------------------------------------------------


************  GÖRÜNÜMLER ( VIEW )  ************


1-) Öğretmenlerin ve iletişim bilgilerinin tek seferde çekildiği view 'dir.


```MYSQL
CREATE VIEW TeacherInfoWithContactView AS
SELECT
    p.FirstName AS 'First Name',
    p.LastName AS 'Last Name',
    p.Gender,
    p.DateOfBirth AS 'Date of Birth',
    t.TeacherId,
    t.Branch,
    t.StartingDate,
    ci.PhoneNumber,
    ci.Email,
    ci.Address
FROM Teachers t
JOIN Persons p ON t.PersonId = p.Id
JOIN ContactInformations ci ON p.ContactId = ci.Id;
```


2-) Tüm öğrencilerin bilgilerini gösteren view 'dir.


```MYSQL
CREATE VIEW StudentInfoView AS
SELECT
    p.FirstName AS 'First Name',
    p.LastName AS 'Last Name',
    p.Gender,
    p.DateOfBirth AS 'Date of Birth',
    s.StudentId,
    s.IsActive,
    s.NOTE
FROM Students s
JOIN Persons p ON s.PersonId = p.Id;
```

Bu kod ile de view kullanılmaktadır.

```MYSQL
SELECT * FROM StudentInfoView;
```
