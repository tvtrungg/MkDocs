---
title: "Frontend Interview"
---

# Mục lục

## **1. Callback**

Là hàm được truyền qua đối số khi gọi hàm khác và được gọi lại trong hàm nhận đối số

```javascript
function myFunc(param){
		param('Hello');
	}

function myCallBack(value){
console.log('Value', value)
}

myFunc(myCallBack);  --> Hello
```

## **2. Promise** - Có từ ES6

- **sync** : đồng bộ --> thằng nào viết trước thì chạy trước

  VD:

  ```javascript
  console.log(1)
  console.log(2)
  --> In ra 1 trước và 2 sau
  ```

- **async**: bất đồng bộ (setTimeout, setInterval, fetch, xml, file reading, req animation)
  `javascript
	setTimeout(function(){
		console.log(1);
	,1000});
	console.log(2);
	--> In 2 trước và 1 sau
	`
  ==> Và để chúng ta biết các thao tác trên khi nào xong
  thì JS cung cấp cho chúng ta Callback để xử lý.
- Tuy nhiên nó sẽ xảy ra vấn đề --> Promise sinh ra để xử lý điều này

### **Promise (pain)**

- **Callback Hell**
  ![Alt text](image.png)

  --> Các dữ liệu ràng buộc với nhau sinh ra callback hell

### **Promise (concept)**

```javascript
var promise = new Promise( // Promise: Object Constructor
  // Executor
  function (resolve, reject) {
    // Logic
    // Success --> gọi resolve() và thất bại --> reject()
  }
);

promise
  .then(function () {}) // Được gọi khi resolve() được gọi
  .catch(function () {}) // Được gọi khi reject() được gọi
  .finally(function () {}); // Đều được gọi
```

- 3 trạng thái của promise:

  - **Pending**: Trạng thái chờ thành công hay thất bại --> nếu chạy hoài thì bị memory leak
  - **Fulfilled**: Trạng thái thành công
  - **Rejected**: Trạng thái thất bại

- Tính chất chuỗi

```javascript
promise
  .then(function (data) {
    return 1;
  })
  .then(function (data) {
    // data: 1 (nhận từ hàm 1)
    console.log(data);
    return 2;
  })
  .then(function (data) {
    // data: 2 (nhận từ hàm 2)
    console.log(data);
    return 3;
  })
  .catch(function () {}) // Được gọi khi reject() được gọi
  .finally(function () {}); // Đều được gọi
```

## **3. JQuery Ajax**

- AJAX - "Asynchronous JavaScript and XML" - là một bộ công cụ cho phép load dữ liệu từ server mà không yêu cầu tải lại trang. Nó sử dụng chức năng sẵn có XMLHttpRequest(XHR) của trình duyệt để thực hiện một yêu cầu đến server và xử lý dữ liệu server trả về.
- jQuery cung cấp method **$.ajax** và một số methods tiện lợi giúp bạn làm việc với XHRs thông qua trình duyệt một cách dễ dàng hơn.

  - `a) Phương thức “load()”`

    - Cú pháp:

    ```javascript
    [selector].load(URL, [data], [callback]);
    ```

    - Ví dụ:

    ```javascript
    $(document).ready(function() {
            $("#driver").click(function(event){
                $('#stage').load('./result.html');
            });
    });

    <div id="stage">STAGE</div>
        <input type="button" id="driver" value="Load Data" />
    ```

    --> Hàm load() khởi tạo một AJAX request tới URL file đã xác định là ./result.html. Sau khi tải file này, tất cả nội dung sẽ được đưa đến vào trong phần tử được tag với ID là stage.

  - `b) Phương thức “get()” và “post()”`

    - get()

    ```javascript
    $(document).ready(function () {
      $("#load-du-lieu").click(function (e) {
        e.preventDefault();
        $.get("vidu1.html", function (ketqua) {
          $("#noidung").html(ketqua);
          $("#noidung").html($("#chuoi-can-lay").html());
        });
      });
    });
    ```

    - post()

    ```javascript
    $(document).ready(function () {
      $("#load-du-lieu").click(function (e) {
        e.preventDefault();
        $.post(
          "vidu2.php",
          {
            a: "content abc",
            b: "content bcd",
          },
          function (ketqua) {
            $("#noidung").html(ketqua);
          }
        );
      });
    });
    ```

  - `c) Phương thức “ajax()”`

  ```javascript
  $(document).ready(function () {
    $("#load-du-lieu").click(function (e) {
      e.preventDefault();
      $.ajax({
        url: "vidu2.php",
        type: "POST",
        dataType: "html",
        data: {
          a: "content abc",
          b: "content bcd",
        },
      }).done(function (ketqua) {
        $("#noidung").html(ketqua);
      });
    });
  });
  ```

  Đối số đầu tiên chúng ta truyền vào cho phương thức “ ajax() ” chính là một đối tượng (Object) gồm các thuộc tính cấu hình để kĩ thuật AJAX của chúng ta có thể thực thi. Trong đó:

  - **url** : chuỗi chứa đường dẫn tới file cần lấy và trả về dữ liệu
  - **type** : phương thức gửi đi tương tự như của `<form>`, mặc định là “GET” nếu như các bạn không truyền vào.
  - **dataType** : xác định dữ liệu trả về thuộc dạng nào? Nếu các bạn không truyền thì jQuery tự động nhận biết kiểu dữ liệu (script, html, json…). Tuy nhiên, tôi khuyến cáo các bạn nên truyền vào đầy đủ để nhận dữ liệu chính xác nhất. Và thông dụng nhất chính là “html”.
  - **data** : truyền dữ liệu sang đường dẫn chỉ định để thực hiện xử lý và trả về dữ liệu. Tương tự như cách truyền dữ liệu của phương thức “ post() ”.
  - **“done()”** : ở loạt các bài viết hướng dẫn các bài viết về kĩ thuật Ajax với phương thức “ ajax() ” trước đây trên Internet. Thay vì dùng “done()” chúng ta sẽ dùng thuộc tính “success” trong đối tượng truyền vào “ ajax() ” nhưng từ các phiên bản mới hơn của jQuery. Họ khuyến cáo chúng ta nên sử dụng các phương thức như “ done() , fail() , always() ” (Tương ứng: Hoàn thành, thất bại và luôn luôn thực hiện). Nên tùy vào nhu cầu mà bạn xài phương thức tương ứng. Và nên nhớ là đi kèm với phương thức “ ajax() ” hoặc lưu vào một tên biến rồi dùng sau để nhận kết quả trả về.

## **4. XML**

- Trong lập trình ứng dụng web, XML được sử dụng nhiều nhất là xây dựng các API Service. Các API sẽ trả kết quả về dạng XML hoặc JSON để các hệ thống khác có thể nói nói chuyện với nhau được. Hiện nay tuy JSON được sử dụng phổ biến hơn, nhưng XML cũng vẫn đang được dùng bởi nhiều hệ thống lớn.

- XML là gì?

  - XML là từ viết tắt của từ Extensible Markup Language là ngôn ngữ đánh dấu mở rộng. XML có chức năng truyền dữ liệu và mô tả nhiều loại dữ liệu khác nhau. Tác dụng chính của XML là đơn giản hóa việc chia sẻ dữ liệu giữa các nền tảng và các hệ thống được kết nối thông qua mạng Internet.

  - XML dùng để cấu trúc, lưu trữ và trong trao đổi dữ liệu giữa các ứng dụng và lưu trữ dữ liệu. Ví dụ khi ta xây dựng một ứng dụng bằng Php và một ứng dụng bằng Java thì hai ngôn ngữ này không thể hiểu nhau, vì vậy ta sẽ sử dụng XML để trao đổi dữ liệu. Chính vì vậy, XML có tác dụng rất lớn trong việc chia sẻ, trao đổi dữ liệu giữa các hệ thống.

## **5. Regex**

![Alt text](image-1.png)

Ví dụ

- Phương thức exec được dùng để tìm chuỗi phù hợp theo mẫu so khớp.

  ```javascript
  var myRe = /d(b+)d/g;
  var myArray = myRe.exec("cdbbdbsbz");

  hoặc;

  var myArray = /d(b+)d/g.exec("cdbbdbsbz");
  ```

- Nếu bạn muốn khởi tạo một biểu thức chính quy từ một chuỗi:
  ```javascript
  var myRe = new RegExp("d(b+)d", "g");
  var myArray = myRe.exec("cdbbdbsbz");
  ```

## **6. Restful API**

### **6.1 Restful API**

- RESTful API là một tiêu chuẩn dùng trong việc thiết kế API cho các ứng dụng web (thiết kế Web services) để tiện cho việc quản lý các resource

### **6.2 Các thành phần**

- **API** (Application Programming Interface) là một tập hợp các quy tắc và cơ chế cho phép các ứng dụng hoặc thành phần khác tương tác với nhau. API có thể trả về dữ liệu dạng JSON hoặc XML để ứng dụng của bạn sử dụng.
- **REST** (REpresentational State Transfer) là một kiểu kiến trúc API sử dụng phương thức HTTP để giao tiếp giữa các máy tính. Thay vì sử dụng URL để xử lý thông tin người dùng, REST sử dụng các yêu cầu HTTP như GET, POST, DELETE để thao tác dữ liệu.

- **Chức năng quan trọng nhất** của REST là quy định cách sử dụng các HTTP method (như GET, POST, PUT, DELETE…) và cách định dạng các URL cho ứng dụng web để quản các resource. RESTful không quy định logic code ứng dụng và không giới hạn bởi ngôn ngữ lập trình ứng dụng, bất kỳ ngôn ngữ hoặc framework nào cũng có thể sử dụng để thiết kế một RESTful API.

### **6.3 Hoạt động**

REST hoạt động chủ yếu dựa vào giao thức HTTP. Các hoạt động cơ bản nêu trên sẽ sử dụng những phương thức HTTP riêng.

- GET (SELECT): Trả về một Resource hoặc một danh sách Resource.
- POST (CREATE): Tạo mới một Resource.
- PUT (UPDATE): Cập nhật thông tin cho Resource.
- PATCH (tương tự PUT): Được dùng để thay đổi data, nhưng nó chỉ thay đổi những field được yêu cầu thay đổi thay vì toàn bộ resource.
- DELETE (DELETE): Xoá một Resource.

### **6.4 Authentication và dữ liệu trả về**

RESTful API không sử dụng session và cookie, nó sử dụng một access_token với mỗi request. Dữ liệu trả về thường có cấu trúc như sau:

```json
{
  "data": {
    "id": "1",
    "name": "TopDev"
  }
}
```

### **6.5 Status code**

- 2xx - Thành công
  - 200 - Trả về thành công cho các method
- 3xx - Điều hướng lại hoặc ko thay đổi
  - 304 - Not Modified – Client có thể sử dụng dữ liệu cache.
- 4xx - lỗi client
  - 400 - Request không hợp lệ
  - 404 - Not Found
- 5xx - lỗi server

### **6.6 Authorization**

Hiện tại có 3 cơ chế Authorize chính:

- HTTP Basic
- [JSON Web Token (JWT)](#1-callback)
- OAuth2

## **7. JWT**

### **7.1 Khái niệm**

JWT (JSON Web Token) là một phương tiện đại diện cho các yêu cầu chuyển giao giữa hai bên Client – Server , các thông tin trong chuỗi JWT được định dạng bằng JSON.

![Alt text](image-2.png)

### **7.2 Cấu trúc**

Gồm 3 phần, được ngăn cách nhau bởi dấu chấm (.):

#### **a. Header**

- Phần header sẽ chứa kiểu dữ liệu , và thuật toán sử dụng để mã hóa ra chuỗi JWT

```json
{
  "typ": "JWT",
  "alg": "HS256"
}
```

- **“typ” (type)** chỉ ra rằng đối tượng là một **JWT**
- **“alg” (algorithm)** xác định thuật toán mã hóa cho chuỗi là **HS256**

#### **b. Payload**

Phần payload sẽ chứa các thông tin mình muốn đặt trong chuỗi Token như username , userId , author , … ví dụ:

```json
{
  "user_name": "admin",
  "user_id": "1513717410",
  "authorities": "ADMIN_USER",
  "jti": "474cb37f-2c9c-44e4-8f5c-1ea5e4cc4d18"
}
```

#### **c. Signature**

Phần chử ký này sẽ được tạo ra bằng cách mã hóa phần header , payload kèm theo một chuỗi secret (khóa bí mật) , ví dụ:

```javascript
data = base64urlEncode(header) + "." + base64urlEncode(payload);
signature = Hash(data, secret);
```

- **base64UrlEncoder** : thuật toán mã hóa header và payload

Đoạn code trên sau khi mã hóa header và payload bằng thuật toán base64UrlEncode ta sẽ có chuỗi như sau

```javascript
// header
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9;

// payload
eyJhdWQiOlsidGVzdGp3dHJlc291cmNlaWQiXSwidXNlcl9uYW1lIjoiYWRtaW4iLCJzY29wZSI6WyJyZWFkIiwid3JpdGUiXSwiZXhwIjoxNTEzNzE;
```

Sau đó mã hóa 2 chuỗi trên kèm theo secret (khóa bí mật) bằng thuật toán HS256 ta sẽ có chuỗi signature như sau:

```jwt
9nRhBWiRoryc8fV5xRpTmw9iyJ6EM7WTGTjvCM1e36Q
```

### **7.3 Khi nào nên dùng JWT**

- Authentication: Đây là trường hợp phổ biến nhất thường sử dụng JWT. Khi người dùng đã đăng nhập vào hệ thống thì những request tiếp theo từ phía người dùng sẽ chứa thêm mã JWT. Điều này cho phép người dùng được cấp quyền truy cập vào các url, service, và resource mà mã Token đó cho phép. Phương pháp này không bị ảnh hưởng bởi Cross-Origin Resource Sharing (CORS) do nó không sử dụng cookie.

- Trao đổi thông tin: JSON Web Token là 1 cách thức khá hay để truyền thông tin an toàn giữa các thành viên với nhau, nhờ vào phần signature của nó. Phía người nhận có thể biết được người gửi là ai thông qua phần signature. Và chữ ký được tạo ra bằng việc kết hợp cả phần header, payload lại nên thông qua đó ta có thể xác nhận được chữ ký có bị giả mạo hay không.

## **8. Phân biệt Authentication và Authorization**

- Authentication (xác thực người dùng)
- Authorization (các quyền của người dùng)
  ![Alt text](image-3.png)

### **8.1 Các phương thức phổ biến dùng authentication**

#### **a. Basic Authentication**

- Đây là phương thức xác thực **ít được khuyến khích** bởi tình bảo mật của nó không an toàn.
- Dễ thực hiện
- Người gửi (sender) sẽ gửi username, password của mình trong _header_ của request. Username và password phải được mã hóa dưới dạng Base64 để đảm bảo tính an toàn hơn.
- Với phương thức này _có thể không cần yêu cầu_ về cookies, session ID... bởi vì chỉ cần sử dụng với http header, không cần đến hỗ trợ từ response khác.
  ```javascript
  Authorization: Basic bG9sOnNlY3VyZQ==
  ```

#### **b. Bearer Authentication**

- Còn được gọi là token authentication
- Có thể hiểu đơn giản là "cấp quyền truy cập cho người mang (bearer) token này".
- Bearer token sẽ cho phép truy cập đến một số tài nguyên hoặc url nhất định và thường là một chuỗi string được mã hóa, được sinh ra bởi server trong response để thực hiện request login.
- Khi thực hiện bằng phương thức này thì client phải gửi bearer token này trong header để thực hiện request
  `javascript
	Authorization: Bearer <token>
	`
  **- Quá trình:**

1. User gửi request -> server để lấy một token bằng username, password thông qua SSL, server sẽ trả về một chuỗi access token.
2. Access token này chính là bearer token mà client cần phải gửi vào header nếu muốn thực hiện các request khác để server xác thực user đó là đúng.
   - Token này có thể là một chuỗi mã hóa với các thuộc tính của user, vai trò của user đó.
   - Khi server nhận được token này, sẽ giải mã sau đó sẽ thực hiện validate request đó trong ứng dụng xem user có được quyền thực hiện request đó hay không.
   - Token này thường sẽ có hạn (ví dụ: 30 phút sau khi lấy sẽ hết hạn) bởi vì có thể role của user sẽ thay đổi trong quá trình thực hiện. Sẽ có trường hợp ví dụ user đang có role="Admin" chuyển thành "User".
   - Nếu token không hết hạn thì token cũ với role="Admin" vẫn có quyền truy cập với role đó mặc dù đã bị thay đổi.

#### **c. API Keys**

- Được tạo ra để khắc phục những vấn đề của basic authentication.
- Trong phương thức này, một giá trị key duy nhất sinh (unique key) ra và gán cho user trong lần đầu tiên, biểu thị rằng user đó được xác định.
- Khi user quay trở lại hệ thống, unique key được sử dụng để chứng minh rằng user là giống với lần đầu tiên.

#### **d. OAuth (2.0)** - Open với Authentication hoặc Authorization

- Ra đời nhằm giải quyết các vấn đề trên và xa hơn nữa, đây là một phương thức chứng thực giúp các ứng dụng có thể chia sẻ tài nguyên với nhau mà không cần chia sẻ thông tin username và password. - OAuth bao gồm bốn vai trò khác nhau: - **Resource Server**: REST API là một ví dụ, một máy chủ HTTP nơi người dùng có thể tạo, sửa đổi hoặc xóa các bản ghi, tài liệu hoặc tệp.

      - **Resource Owner**:
      	- Duy trì *quyền sở hữu tài nguyên* mà người dùng đã tạo hoặc sửa đổi trên máy chủ
      	- *Quyền truy cập hạn chế* của bên thứ 3 vào tài khoản của người dùng, dựa trên phạm vi của phạm vi của ủy quyền được cấp.

      - **Client**:
      	- Ứng dụng bên thứ 3 muốn truy cập vào tài khoản người dùng. <br>
      	--> Bắt buộc máy chủ resource/authorization và chủ sở hữu tài nguyên phải **ủy quyền** cho yêu cầu đó.
      	- Mọi khách hàng phải được đăng ký với máy chủ authorization và sẽ được cung cấp thông tin xác thực duy nhất của riêng mình (client_id và client_secret).

      - **Authorization Server** (thường là giống Resource Server): Đôi khi, ta có thể muốn rút ra khỏi máy chủ authorization từ máy chủ resource và triển khai nó như một phiên bản chuyên dụng, đặc biệt là trong các môi trường phân tán.

      - **Ví dụ:**<br>
      	- Khi ta đăng nhập bằng Facebook hay Gmail, website sẽ dẫn ta đến trang (hoặc phần mềm) Facebook và liệt kê những quyền mà nó cần phải có để cho phép bạn đăng nhập và sử dụng dịch vụ.
      	- Nếu ta *đồng ý* thì lúc này Facebook sẽ phát cho website một cái token(chứa một số quyền hạn nhất định giúp cho website có thể xác minh chúng ta là ai cũng như giúp cho website có thể hoạt động được).
      	- Nếu website này bị hacker tấn công thì nó chỉ lấy được thông tin hay hoạt động của ta trên website đó mà không ảnh hưởng đến những website khác đang sử dụng.

      `--> Do đó cách đăng nhập bằng phương thức OAuth này rất an toàn cho người dùng cuối như chúng ta.

  `

## **9. SPA và MPA**

### **9.1 SPA - Single-Page Application**

- ReactJS là 1 trong những thư viện tạo ra SPA
- Các "ông lớn" sử dụng SPA : Google, Facebook, Twitter
- Các SPA khác : F8, Shoppe, 30shine, chotot, zingmp3
- Single-Page đang nói đến kiến trúc phía bên dưới, chứ không phải là Web 1 trang dưới mắt nhìn người dùng

### **9.2 Cách triển khai**

- SPA - Single-Page Application -> CSR --> Client side rendering
- MPA - Multi-Page Application -> SSR --> Server side rendering

### **9.3 Sự khác biệt**

- SPA :

  - Được cho là cách tiếp cận hiện đại hơn
  - Không yêu cầu tải lại trang trong quá trình sử dụng

- MPA:
  - Cổ điển
  - Tải lại trang trong QT sử dụng (click vô đường link, chuyển sang,...)
  - Thường dùng php, nodejs,...

### **9.4 So sánh**

- Tốc độ
  - SPA nhanh hơn khi sử dụng
    - Phần lớn tài nguyên được tải trong lần đầu (Có thể chậm hơn lần đầu)
    - Trang chỉ tải thêm dữ liệu mới khi cần
  - MPA chậm hơn khi sử dụng
    - Luôn tải lại toàn bộ trang khi truy cập và chuyển hướng
- Bóc tách
  - SPA có phần Front-end riêng biệt
  - MPA Front-end & Back-end phụ thuộc nhau nhiều hơn, được đặt trong cùng 1 dự án
  - Mô hình MVC (controller, views,...)
- SEO (Search Engine Optimization - Tối ưu hóa công cụ tìm kiếm)

  - SPA không thân thiện với SEO như MPA
  - Trải nghiệm trên thiết bị di động tốt hơn

- UX (User Experience)

  - SPA cho trải nghiệm tốt hơn, nhất là các theo tác chuyển trang
  - Trải nghiệm trên thiết bị di động tốt hơn

- Quá trình phát triển
  - SPA dễ dàng tái sử dụng code (component)
  - SPA bóc tách FE & BE
    - Chia team phát triển song song
    - Phát triển thêm mobile app dễ dàng 14

## **10. SSR và CSR**

### **10.1 SSR (server side render):**

- Request các API để trả về từ server -> Sau đó trình duyệt render ra
- Ưu điểm:
  - tốt cho seo, tăng thứ hạng cho website (dantri, tintuc,...)
  - Request đầu tiên đa phần sẽ nhanh hơn
  - Phát triển ứng dụng nhanh hơn SSR (các ứng dụng nhỏ)
- Khuyết điểm:
  - Reload cả trang khi chuyển hướng

### **10.2 CSR (Client side render):**

- Vẫn có 1 chút SSR (render thẻ div trống `<main>`)
- Bên client sẽ đọc các file js rồi render ra (trình duyệt phải bật chức năng js, nếu tắt đi --> die)
- Như Reactjs (chuyển trang ko cần load lại full trang)
- Ưu điểm:
  - Chuyển trang mượt mà (ko cần reload cả trang)
- Khuyết yếu:
  - Request đầu tiên sẽ chậm hơn
  - Không đọc được nội dung trang tin tức, ko mang tính seo (các trang thời sự, tin tức sẽ ko dùng CSR)

## **11. Lazy loading**

### **11.1 Khái niệm**

- Là 1 kĩ thuật tối ưu khi làm web, thay vì tải toàn bộ trang web và render ngay từ đầu, kỹ thuật này cho phép tải ngay các thành phần cần thiết để hiển thị tới người dùng và trì hoãn các tài nguyên còn lại cho đến khi cần.
- Ưu điểm: Tối ưu hiệu suất web, đỡ tốn tài nguyên, băng thông,...

### **11.2 Ứng dụng**

- Được sử dụng rộng rãi nhất trong lập trình, thiết kế website.
- WordPress cung cấp một giải pháp dựa trên Lazy Loading mang tên Infinite Scroll, hỗ trợ bạn sử dụng con lăn và cuộn con chuột liên tục để đọc thêm các nội dung mới.
- Google tiếp cận với Lazy loading theo hướng cụ thể là ở mục tìm kiếm hình ảnh. Google sẽ đưa ra danh sách 4-5 bức ảnh liên quan sau khi xem cụ thể một tấm hình nào đó và bên cạnh đó là nút “View More” để xem nhiều ảnh hơn.

### **11.3 Các kỹ thuật cơ bản**

- Thêm thuộc tính loading với giá trị lazy:

  ```html
  <img src="awesome-photo.jpg" loading="lazy" />
  ```

  - Dưới đây là các giá trị được hỗ trợ cho thuộc loading:

    - **auto**: Giá trị mặc định phụ thuộc vào hành vi của từng trình duyệt, tương tự với việc không thêm thuộc tính loading vào.
    - **lazy**: Trì hoãn tải tài nguyên về cho đến khi đạt 1 khoảng cách nào đó từ khung nhìn.
    - **eager**: Tải tài nguyên ngay lập tức, bất kể vị trí của nó trên trang.

  - Đối với các trình duyệt chưa hỗ trợ thì có thể tạo polyfill hoặc dùng thư viện bên thứ 3 như [LazySizes](https://github.com/aFarkas/lazysizes)

- ### [LazySizes](https://github.com/aFarkas/lazysizes)
  - Là thư viện có tốc độ cao, tối ưu SEO và tự khởi tạo (self-initializing) cho mục đích lazy load ảnh (bao gồm cả ảnh đáp ứng picture / srcset), iframe, script / widget và nhiều thành phần khác nữa.
  - Nó cũng ưu tiên các tài nguyên dựa trên sự khác biệt về tầm mức quan trọng, trong đó. LazySizes ưu tiên các phần tử nằm trong khung nhìn và gần khung nhìn trình duyệt (near view elements) để tối ưu tốc độ tải nhận thức (perceived performance) nhanh hơn.

## **12. Mô hình MVC**

## **13. Mô hình MVP**

## **14. Mô hình MVVM**

## **15. So sánh 3 mô hình MVC, MVP, MVVM**

| Mô hình | Mô tả                                                                                                                                                                              | Ưu điểm                                                                                     | Nhược điểm                                                                                                                                  |
| ------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------- |
| MVC     | `Model-View-Controller (MVC)` chia thành ba thành phần chính: Model (dữ liệu), View (giao diện) và Controller (xử lý logic).                                                       | - Phân chia rõ ràng giữa các thành phần, tạo sự tách biệt giữa dữ liệu, giao diện và logic. | - Đôi khi Controller có thể trở nên phức tạp và quá mức phụ thuộc vào View và Model.                                                        |
| MVP     | `Model-View-Presenter (MVP)` cũng chia thành ba thành phần chính: Model (dữ liệu), View (giao diện) và Presenter (xử lý logic và trung gian giữa Model và View).                   | - Giúp tách biệt logic xử lý và giao diện, dễ dàng kiểm thử đơn vị.                         | - Có sự phụ thuộc mạnh mẽ giữa Presenter và View, có thể dẫn đến khó khăn khi thay đổi giao diện.                                           |
| MVVM    | `Model-View-ViewModel (MVVM)` tách biệt hoàn toàn giữa giao diện (View) và logic (ViewModel) bằng cách sử dụng Data Binding. Model chịu trách nhiệm về dữ liệu và logic nghiệp vụ. | - Data Binding giữa View và ViewModel giúp tự động cập nhật giao diện khi dữ liệu thay đổi. | - Cần sử dụng thêm một số công cụ hoặc thư viện hỗ trợ Data Binding. Có thể dẫn đến hiệu suất chậm nếu không quản lý tốt quá trình binding. |

## **16. Local Storage, Session Storage và Cookie**

### **Giống nhau**

- Đều lưu trữ dữ liệu trên trình duyệt web của người dùng.
- Hỗ trợ lưu trữ dữ liệu ở dạng key-value pairs.
- Có giới hạn dung lượng lưu trữ.
- Chỉ lưu trữ dữ liệu ở dạng chuỗi.

### **Khác nhau**

| Feature                     | Local Storage                                                                                                                        | Session Storage                                                                                                                        | Cookie                                                                                                                                                                                                                        |
| --------------------------- | ------------------------------------------------------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Phạm vi lưu trữ             | Có phạm vi toàn bộ trang web và có thể truy cập từ mọi nơi trên trang web.                                                           | Chỉ có phạm vi trong một phiên làm việc (session) của trình duyệt và bị xóa khi phiên làm việc kết thúc                                | Có thể có phạm vi toàn bộ trang web hoặc chỉ trong một tên miền cụ thể.                                                                                                                                                       |
| Tương tác với máy chủ       | Dữ liệu trong cả hai cơ chế này không được gửi đến máy chủ trong mỗi yêu cầu HTTP. Chúng chỉ tồn tại trên trình duyệt của người dùng | \_                                                                                                                                     | Dữ liệu trong Cookie được gửi đến máy chủ trong mỗi yêu cầu HTTP thông qua header "Cookie". Điều này cho phép máy chủ lưu trữ và đọc dữ liệu từ Cookie.                                                                       |
| Kích thước lưu trữ          | Khoảng 5MB                                                                                                                           | Chỉ vài MB                                                                                                                             | Vài KB                                                                                                                                                                                                                        |
| Thời gian sống              | Không có thời gian sống, nó sẽ tồn tại cho đến khi bị xóa bằng cách xóa bằng tay hoặc thông qua mã lệnh.                             | Chỉ tồn tại trong một phiên làm việc (session) của trình duyệt                                                                         | Có thể có thời gian sống xác định, có thể được đặt để tồn tại trong một khoảng thời gian nhất định hoặc được xóa khi trình duyệt đóng.                                                                                        |
| Sử dụng và mục đích sử dụng | Thường được sử dụng để lưu trữ dữ liệu lâu dài, như cài đặt người dùng, lịch sử truy cập, thông tin cá nhân ...                      | Thường được sử dụng để lưu trữ dữ liệu tạm thời trong phiên làm việc, như thông tin đăng nhập, giỏ hàng, trạng thái phiên làm việc ... | Thường được sử dụng để lưu trữ thông tin nhận dạng người dùng, như thông tin đăng nhập, thông tin ngôn ngữ, thông tin giỏ hàng v.v. Cookie cũng có thể được sử dụng để theo dõi người dùng và cung cấp quảng cáo cá nhân hóa. |

## **17. Khác biệt giữa HTML và HTML5**

HTML5 là phiên bản mới nhất của HTML và cung cấp nhiều tính năng mới như hỗ trợ multimedia, semantic elements, canvas, drag and drop, và offline storage.

## **18. Một số cách tăng Performance website**

Để tối ưu hóa hiệu suất Front-end có thể sử dụng các kỹ thuật như:

- minification và compression của file CSS và JavaScript
- lazy loading, caching, sử dụng sprites hình ảnh, tối ưu hóa đường dẫn và kích thước hình ảnh, và loại bỏ các tài nguyên không cần thiết.

## **19. Tiêu chuẩn W3C**

W3C viết tắt của cụm từ World Wide Web Consortium, W3C là chuẩn được các nhà thiết kế website sử dụng làm thước đo khi thiết kế website, cũng giống như lương của bạn được đo bằng giá trị của bạn mang lại cho công ty vậy.

### **Lợi ích**

- Website của bạn sẽ thân thiện hơn với các Search Engine đặc biệt là google spider.
- Website của bạn được hỗ trợ tốt trên nhiều trình duyệt, bạn không mất nhiều thời gian để chỉnh sửa và tối ưu hóa cho từng trình duyệt.
- Các thiết bị hiển thị website di động như điện thoại IPad đều dựa trên chuẩn W3C. Do đó, Website của bạn sẽ hiển thị tốt hơn. Để kiểm tra website của bạn có tuân thủ theo chuẩn W3C hay chưa thì bạn có thể vào https://validator.w3.org/ để kiểm tra.

### **Một số lưu ý**

- Thiếu thuộc tính alt trên thẻ img
- Đặt giá trị ID trùng nhau
- Sử dụng các ký tự đặc biệt
- Sử dụng sai thuộc tính href trên thẻ a

  ```html
  <a href="”link" 1″ target="”_blank”"> link 1</a>

  --> <a href="”link_1″" target="”_blank”"> link 1</a>
  ```

- Không phân biệt được inline element và block element

## **20. So sánh Javascript ES5 và ES6**

### **Giống nhau**

- Cả ES5 và ES6 đều là phiên bản của JavaScript và chạy trên các trình duyệt hiện đại.
- Cả hai phiên bản hỗ trợ việc xử lý các loại dữ liệu cơ bản, như chuỗi, số, mảng, đối tượng, hàm, và điều khiển luồng.

### **Khác nhau**

| Feature                 | ES5                                                                                                         | ES6                                                                                                                                                                                                                                                                                                                |
| ----------------------- | ----------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| \_                      | Phát hành vào năm 2009                                                                                      | Phát hành vào năm 2015                                                                                                                                                                                                                                                                                             |
| OOP                     | Không hỗ trợ lập trình hướng đối tượng                                                                      | Hỗ trợ lập trình hướng đối tượng                                                                                                                                                                                                                                                                                   |
| Variable                | Sử dụng từ khóa `var` để khai báo biến. Biến khai báo bằng var có phạm vi là hàm và không có phạm vi block. | Hỗ trợ khai báo biến bằng `let` và `const`                                                                                                                                                                                                                                                                         |
| Function                | Cú pháp hàm truyền thống với từ khóa function                                                               | Arrow function (`=>`): là một cú pháp rút gọn của function expression và thừa kế giá trị this từ phạm vi bên ngoài.                                                                                                                                                                                                |
| Template literals       | Sử dụng chuỗi thông thường, hạn chế khả năng kết hợp với biểu thức JavaScript.                              | Cho phép sử dụng template literals (` `` `) để tạo ra chuỗi kết hợp với biểu thức JavaScript một cách dễ dàng và đọc được hơn.                                                                                                                                                                                     |
| Destructuring           | \_                                                                                                          | Là một cú pháp cho phép ta tách các phần tử của một mảng hoặc các thuộc tính của một đối tượng ra và gán chúng vào các biến riêng biệt                                                                                                                                                                             |
| Default parameters      | \_                                                                                                          | Cho phép khai báo giá trị mặc định cho các tham số của hàm, giúp viết mã linh hoạt hơn.                                                                                                                                                                                                                            |
| Rest parameters         | \_                                                                                                          | Là một cú pháp cho phép ta truyền một danh sách các tham số vào một hàm dưới dạng một mảng                                                                                                                                                                                                                         |
| Spread operator         | \_                                                                                                          | Là một cú pháp cho phép ta truyền một mảng vào một hàm dưới dạng một danh sách các tham số.                                                                                                                                                                                                                        |
| Classes                 | Khai báo đối tượng thông qua hàm tạo.                                                                       | Hỗ trợ khai báo lớp thông qua từ khóa `class`, giúp lập trình viên dễ dàng xây dựng và quản lý các đối tượng. <br>`class Person {`<br>&emsp;&emsp;`constructor(name, age) {`<br>&emsp;&emsp;&emsp;&emsp;`        this.name = name;`<br>&emsp;&emsp;&emsp;&emsp;`        this.age = age;`<br>&emsp;&emsp;`}`<br>`}` |
| Modules                 | \_                                                                                                          | Hỗ trợ cú pháp `import` và `export` để nhập và xuất các mô-đun JavaScript, giúp tạo ra cấu trúc mã mô-đun và tái sử dụng mã dễ dàng hơn.                                                                                                                                                                           |
| Promises                | \_                                                                                                          | Đưa vào JavaScript khái niệm Promise để xử lý các tác vụ bất đồng bộ một cách gọn nhẹ và dễ sử dụng hơn.                                                                                                                                                                                                           |
| Iterators và Generators | \_                                                                                                          | Giúp lặp lại và xử lý các tập hợp dữ liệu một cách thuận tiện và linh hoạt.                                                                                                                                                                                                                                        |

## **21. Array Methods**

### **forEach()**

Duyệt qua từng phần tử trong mảng

```javascript
const arr = [1, 2, 3, 4, 5];
arr.forEach((item, index) => {
  console.log(item, index);
});
```

### **every() – bool**

- Kiểm tra tất cả các phần tử trong mảng có thỏa mãn điều kiện hay không.
- Nếu `tất cả các phần tử` đều thỏa mãn điều kiện thì trả về `true`, ngược lại trả về `false`.

```javascript
const arr = [1, 2, 3, 4, 5];
const isEven = arr.every((item) => {
  return item % 2 === 0;
});
console.log(isEven); // false
```

### **some() - bool**

Ngược với `every()`, chỉ cần có 1 ptử đúng --> true

```javascript
const arr = [1, 2, 3, 4, 5];
const isEven = arr.some((item) => {
  return item % 2 === 0;
});
console.log(isEven); // true
```

### **find()**

Trả về phần tử cần tìm `đầu tiên` trong mảng

```javascript
const arr = [1, 2, 3, 4, 5];
const result = arr.find((item) => {
  return item % 2 === 0;
});
console.log(result); // 2
```

### **filter()**

Trả về tất cả ptử cần tìm trong mảng

```javascript
const arr = [1, 2, 3, 4, 5];
const result = arr.filter((item) => {
  return item % 2 === 0;
});
console.log(result); // [2, 4]
```

### **map()**

Có chức năng tương tự như `forEach()`, nhưng `map()` dùng chỉnh sửa các phần tử trong mảng

```javascript
const arr = [1, 2, 3, 4, 5];
const result = arr.map((item) => {
  return item * 2;
});
console.log(result); // [2, 4, 6, 8, 10]

// Ví dụ 2
function courseHandler(course, index) {
  return {
    id: course.id,
    name: ` Khoa hoc: ${course.name}`,
    coin: course.coin,
  };
}

var newCourse = courses.map(courseHandler);
```

### **reduce()**

Dùng để tính tổng các phần tử trong mảng. Hoặc trả về các thông tin của mảng

```javascript
function coinHandler(accumulator, currentValue, currentIndex, array) {
  // accumulator: giá trị trả về của lần gọi trước
  // currentValue: giá trị của phần tử hiện tại
  // currentIndex: index của phần tử hiện tại
  // array: mảng đang được duyệt
  return accumulator + currentValue.coin;
}

var totalCoin = courses.reduce(coinHandler, 0); // 0 là giá trị khởi tạo cho accumulator
```

Ví dụ:

```javascript
// 1. Tính tổng
const arr = [1, 2, 3, 4, 5];
const result = arr.reduce((total, item) => {
  return total + item;
}, 0); // 0 là giá trị khởi tạo cho total
console.log(result); // 15

// 2. Trả về thông tin mảng
var depthArr = [1, 2, [3, 4], 5, 6, [7, 8, 9]];
var flatArr = depthArr.reduce(function (flatOutput, depthItem) {
  return flatOuput.concat(depthItem);
}, []);
console.log(flatArr); // [1, 2, 3, 4, 5, 6, 7, 8, 9]
```

### **concat()**

Dùng để nối 2 mảng lại với nhau

```javascript
const arr1 = [1, 2, 3];
const arr2 = [4, 5, 6];
const result = arr1.concat(arr2);
console.log(result); // [1, 2, 3, 4, 5, 6]
```

### **slice()**

Dùng để cắt mảng

```javascript
const animals = ["ant", "bison", "camel", "duck", "elephant"];

console.log(animals.slice(2)); // ["camel", "duck", "elephant"]

console.log(animals.slice(2, 4)); // ["camel", "duck"]

console.log(animals.slice(1, 5)); // ["bison", "camel", "duck", "elephant"]

console.log(animals.slice(-2)); // ["duck", "elephant"]

console.log(animals.slice(2, -1)); // ["camel", "duck"]
```

### **split()**

Dùng để tách chuỗi thành mảng

```javascript
const str = "Have a good day!";
const result = str.split(" ");
console.log(result); // ["Have", "a", "good", "day!"]
```

### **join()**

Dùng để nối các phần tử trong mảng thành chuỗi

```javascript
const arr = ["Have", "a", "good", "day!"];
const result = arr.join(" ");
console.log(result); // "Have a good day!"
```
