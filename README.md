### البداية والسبب وراء ظهوره ADO.NET


قبل ظهور ADO.NET، كان فيه تكنولوجي اسمها ADO (ActiveX Data Objects) اللي كانت بتُستخدم للتعامل مع Database. لكن مع تطور البرمجة واتجاهها للعمل مع تطبيقات الويب والتطبيقات ال Distributed، ظهرت مشاكل مع ADO زي:

### مشكلة الأداء
كان بيعتمد على (Connected Mode)، يعني لازم يكون فيه اتصال مستمر بقاعدة البيانات أثناء كل العمليات، وده كان بيستهلك موارد النظام بشكل كبير.

ما كانش مرن مع التطبيقات اللي بتحتاج تتعامل مع البيانات بطريقة منفصلة (Disconnected Mode).

ظهرت ADO.NET كجزء من NET Framework. بهدف تحسين الأداء وتقديم دعم أفضل.

### الفرق بين ADO و ADO.NET
| **الميزة**                 | **ADO**                                               | **ADO.NET**                                           |
|----------------------------|-------------------------------------------------------|------------------------------------------------------|
| **السنة**                  | 1996                                                  | مع ظهور .NET Framework                               |
| **النظام المستخدم**         | COM (Component Object Model)                          | CLR (Common Language Runtime) في .NET                 |
| **طريقة الاتصال بقاعدة البيانات** | متصل دائماً بقاعدة البيانات (Connected Mode)         | يمكن العمل بدون اتصال دائم بقاعدة البيانات (Disconnected Mode) |
| **البيانات المُعتمدة**       | "Recordset" لحفظ البيانات وعرضها                    | "Dataset" و"DataRelation" لربط البيانات والجداول بسهولة |
| **دعم XML**                 | لا يدعم XML                                           | يدعم XML بشكل كامل                                  |
| **التعقيد**                 | معقد نسبياً ولا يدعم التقنيات الحديثة                 | أسهل وأكثر مرونة مع دعم تقنيات حديثة مثل XML       |



### متى نستخدم Connected Mode؟
- لما تكون البيانات اللي محتاجها بتتغير بسرعة وعايز أحدث نسخة.
- لما تكون البيانات بسيطة ومش محتاج تعدل عليها كتير.
#### الأمثلة:
- تطبيق عرض أسعار الأسهم اللي بيحتاج تحديث مستمر وفوري للبيانات.
- تنفيذ عمليات سريعة على قاعدة البيانات بدون تخزين مؤقت.
- لوحة تحكم بتعرض بيانات في الوقت الحقيقي مثل بيانات مستشعرات (Sensors).
 - ***الobject المستخدم SqlDataReader.***

### متى نستخدم Disconnected Mode؟
- لما تكون شغال على تطبيق فيه عدد كبير من المستخدمين وما ينفعش كلهم يبقوا متصلين بقاعدة البيانات طول الوقت.
- لما تكون عايز تعمل تعديلات على البيانات بعيد عن قاعدة البيانات ثم ترجعها بعد كدا.
- تطبيق لإدارة الحجوزات في فندق، حيث بيتم تحميل بيانات العملاء والعمل عليها بدون الحاجة لاتصال دائم بقاعدة البيانات.
#### الأمثلة:
- تطبيقات إدارة المبيعات اللي بتحمل بيانات العملاء مرة واحدة وتعدل عليها بدون اتصال مستمر.
- تقارير Excel اللي بتعتمد على بيانات قاعدة البيانات ولكن بتشتغل عليها بشكل منفصل.
- ***الobject المستخدم SqlDataAdapter.***
### اي هو ADO.Net
هي مجموعة من الـ classes اللي بتسهل التعامل مع قواعد البيانات في برامجك اللي بتستخدم .NET. يعني لو عايز تتعامل مع قاعدة بيانات (سواء كان SQL Server أو أي نوع تاني من قواعد البيانات)، ممكن تستخدم الأدوات دي عشان تسهل عليك إزاي تضيف وتعدل وتسترجع بيانات.

في الـ ADO.NET، في كلاس رئيسي زي SqlConnection عشان تتصل بقاعدة البيانات، وSqlCommand عشان تنفذ الاستعلامات، وSqlDataReader عشان تقرأ البيانات اللي جايه من الاستعلام. فالفكرة كلها إنك مش مضطر تتعامل مع التفاصيل الكثيرة بنفسك، الـ ADO.NET بيسهل عليك الموضوع ده.



# مكونات ADO.NET بالتفصيل

## 1. SqlConnection
ده الكائن اللي بيسمح بفتح اتصال مع قاعدة البيانات. لازم تحدد بيانات الاتصال زي:
- اسم الخادم (Server Name).
- اسم قاعدة البيانات.

## 2. SqlCommand
ده الكائن اللي بنستخدمه لتنفيذ الأوامر على قاعدة البيانات زي:
- SELECT
- INSERT
- UPDATE
- DELETE

بيربط مع SqlConnection عشان يعرف أي قاعدة بيانات يتعامل معها.

## 3. SqlDataReader
ده بيشتغل في وضع Connected Mode. بيجيب البيانات في شكل (Stream) للقراءة فقط، وده بيخلي الأداء سريع جدًا.

## 4. DataSet
ده عبارة عن "نسخة مؤقتة" من البيانات بتتخزن في الذاكرة. يحتوي على:
- جداول (DataTables)
- وصفوف (Rows)
- أعمدة (Columns)
كأنه قاعدة بيانات صغيرة. بيدعم الوضع Disconnected Mode، وده بيخليك تعدل على البيانات بدون الحاجة للاتصال المستمر بقاعدة البيانات.

## 5. SqlDataAdapter
ده بيعمل دور الوسيط بين DataSet وقاعدة البيانات. بيملأ DataSet بالبيانات ويكتب التعديلات مرة تانية في قاعدة البيانات. بيستخدم كائنات SqlCommand لتنفيذ العمليات.

# أكواد ADO.NET

## 1. SqlConnection
```csharp
using System;
using System.Data.SqlClient;

class Program
{
    static void Main()
    {
        // هنا بنكتب بيانات الاتصال بقاعدة البيانات
        string connectionString = "Server=.;Database=YourDatabase;Trusted_Connection=True;TrustServerCertificate=True;";
        
        // ده الكائن اللي هيعمل الاتصال بقاعدة البيانات
        SqlConnection connection = new SqlConnection(connectionString);

        try
        {
            // هنفتح الاتصال بقاعدة البيانات
            connection.Open();
            
            // هنطبع اسم قاعدة البيانات اللي متصلين بيها
            Console.WriteLine($"Database: {connection.Database}");
            
            // هنطبع اسم السيرفر اللي متصلين عليه
            Console.WriteLine($"Server: {connection.DataSource}");
            
            // هنطبع الوقت المسموح بيه للاتصال قبل ما يفصل (بالثواني)
            Console.WriteLine($"Connection Timeout: {connection.ConnectionTimeout}");
            
            // هنطبع حالة الاتصال دلوقتي (هل هو مفتوح ولا مقفول)
            Console.WriteLine($"State: {connection.State}");
            
            // هنقفل الاتصال بقاعدة البيانات
            connection.Close();
            
            // هنطبع حالة الاتصال بعد ما قفلناه
            Console.WriteLine($"State after Close: {connection.State}");
        }
        catch (Exception ex)
        {
            // لو حصل خطأ، هنعرض رسالة الخطأ
            Console.WriteLine($"An error occurred: {ex.Message}");
        }
    }
}

```
## 2. SqlCommand
```csharp
using System;
using System.Data.SqlClient;

class Program
{
    static void Main()
    {
        // بيانات الاتصال بقاعدة البيانات
        string connectionString = "Server=.;Database=YourDatabase;Trusted_Connection=True;TrustServerCertificate=True;";

        // استعلام الإضافة
        string insertQuery = "INSERT INTO Users (Name, Age) VALUES (@Name, @Age)";

        // تجهيز كائن الاتصال
        SqlConnection connection = new SqlConnection(connectionString);

        // تجهيز كائن الأمر وربطه بالاتصال
        SqlCommand command = new SqlCommand(insertQuery, connection);

        // إضافة القيم للباراميترز
        command.Parameters.AddWithValue("@Name", "Eman Elsayed");
        command.Parameters.AddWithValue("@Age", 22);

        try
        {
            // فتح الاتصال بقاعدة البيانات
            connection.Open();

            // تنفيذ استعلام الإضافة
            int rowsAffected = command.ExecuteNonQuery();

            // طباعة عدد الصفوف اللي تم إضافتها
            Console.WriteLine($"{rowsAffected} صفوف تم إضافتها بنجاح.");
        }
        catch (Exception ex)
        {
            // لو حصل خطأ، نعرض رسالة الخطأ
            Console.WriteLine($"خطأ أثناء إضافة البيانات: {ex.Message}");
        }
        finally
        { // التأكد من إغلاق الاتصال بقاعدة البيانات
            if (connection.State == System.Data.ConnectionState.Open)
            {
                connection.Close();
                Console.WriteLine("تم إغلاق الاتصال بقاعدة البيانات.");
            }
        }
    }
}
```
## 3. DataReader
```csharp
using System;
using System.Data.SqlClient;

class Program
{
    static void Main()
    {
        // بيانات الاتصال بقاعدة البيانات
        string connectionString = "Server=.;Database=YourDatabase;Trusted_Connection=True;TrustServerCertificate=True;";

        // الاستعلام اللي هنستخدمه لجلب البيانات
        string query = "SELECT Id, Name, Age FROM Users";

        // تجهيز كائن الاتصال
        SqlConnection connection = new SqlConnection(connectionString);

        // تجهيز كائن الأمر (Command)
        SqlCommand command = new SqlCommand(query, connection);

        try
        {
            // فتح الاتصال بقاعدة البيانات
            connection.Open();

            // تنفيذ الاستعلام وجلب البيانات باستخدام SqlDataReader
            SqlDataReader reader = command.ExecuteReader();

            // قراءة البيانات من SqlDataReader وعرضها
            while (reader.Read())
            {
                // طباعة كل صف من البيانات
                Console.WriteLine($"ID: {reader["Id"]}, Name: {reader["Name"]}, Age: {reader["Age"]}");
            }

            // التأكد من إغلاق الـ SqlDataReader بعد الاستخدام
            reader.Close();
        }
        catch (Exception ex)
        {
            // لو حصل خطأ هنطبع رسالة الخطأ
            Console.WriteLine($"خطأ أثناء قراءة البيانات: {ex.Message}");
        }
        finally
        {
            // التأكد من إغلاق الاتصال بقاعدة البيانات
            if (connection.State == System.Data.ConnectionState.Open)
            {
                connection.Close();
                Console.WriteLine("تم إغلاق الاتصال بقاعدة البيانات.");
            }
        }
    }
}
```
## 4. DataAdapter
```csharp
using System;
using System.Data;
using System.Data.SqlClient;

class Program
{
    static void Main()
    {
        // بيانات الاتصال بقاعدة البيانات
        string connectionString = "Server=.;Database=YourDatabase;Trusted_Connection=True;TrustServerCertificate=True;";
        
        // الاستعلام اللي هيجيب البيانات من جدول Users
        string query = "SELECT Id, Name, Age FROM Users";
        
        // تجهيز كائن DataTable علشان نخزن فيه البيانات المسترجعة
        DataTable datatable = new DataTable();
        
        // فتح الاتصال بقاعدة البيانات
        using (SqlConnection connection = new SqlConnection(connectionString))
        {
            // تجهيز SqlDataAdapter اللي هيجيب البيانات من الاستعلام ويروح يحطها في الـ DataTable
            SqlDataAdapter adapter = new SqlDataAdapter(query, connection);

            try
            {
                // ملء الـ DataTable بالبيانات من قاعدة البيانات
                adapter.Fill(datatable);

                // نقرأ البيانات من الـ DataTable ونعرضها
                foreach (DataRow row in datatable.Rows)
                {
                    // طباعة البيانات لكل صف
                    Console.WriteLine($"ID: {row["Id"]}, Name: {row["Name"]}, Age: {row["Age"]}");
                }
            }
            catch (Exception ex)
            {
                // لو حصل خطأ في جلب البيانات، هنطبع رسالة الخطأ
                Console.WriteLine($"خطأ أثناء جلب البيانات: {ex.Message}");
            }
        }
    }
}
```




