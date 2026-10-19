# 5.1 Feed-forward Network Functions

📊 **Progress:** `4` Notes | `8` Screenshots | `4` AI Reviews

---
<a id="node-hb0d5sh"></a>

<br>

<a id="node-ks8plop"></a>

## Feed-forward Network Functions

<p align="center"><kbd><img src="assets/wkfi849uc5a.png" width="80%"></kbd></p>

<p align="center"><kbd><img src="assets/jpzfi2rmmln.png" width="80%"></kbd></p>

<p align="center"><kbd><img src="assets/9fr06c4p8t9.png" width="80%"></kbd></p>

<p align="center"><kbd><img src="assets/9ia8ft9353u.png" width="80%"></kbd></p>

> [!NOTE]
> Đại khái là trong chapter 3, linear model cho bài toán regression là và cho bài toán classification để có thể nói là có dạng chung là f(𝐰ᵀΦ(𝐱)) = f(Σj wj φj(𝐱)). f là non-linear activation function, với regression, f là identity function.
>
>
>
> Là sao: Nhớ lại:
>
>
>
> Trong chương 3: Ta giả định T|𝐱 \~ 𝒩(𝐰ᵀΦ(𝐱), 1/β), giả định T|𝐱 là normal có phương sai cố định và conditional expectation E\[T|𝐱\] là hàm tuyến tính theo 𝐰 (nên mới gọi là linear regression) và phi tuyến đối với 𝐱 (mà theo sách thống kê casella, cái này gọi là regression của T on 𝐱 là non-linear): f(𝐰ᵀΦ(𝐱)) với f(u) = u
>
>
>
> Chương 4 tương tự, ở binary classification, ta giả định P(𝒞=𝒞1|𝐱) = σ(𝐰ᵀΦ(𝐱))
>
>
>
> Vậy thì cả hai đều có dạng f(𝐰ᵀΦ(𝐱)) (với regression thì f là identity) 
>
>
>
> hàm f áp lên linear combination của các φ1(𝐱),φ2(𝐱),...với hệ số tổ hợp là w1,w2,...(có thêm bias w0 nữa nhưng tạm bỏ qua đi).
>
>
>
> Regression: y(𝐱, 𝐰) = f(w1 φ1(𝐱) + w2 φ2(𝐱) + ...wM φM(𝐱)) = 𝐰ᵀΦ(𝐱)
>
>
>
> hay binary class classification
>
>
>
> y(𝐱, 𝐰) = σ(w⁽²⁾1 φ1(𝐱) + w⁽²⁾2 φ2(𝐱) + ...w⁽²⁾M φM(𝐱)) = σ(𝐰ᵀΦ(𝐱))
>
>
>
> hay multiple class classification:
>
>
>
> y1 = σ(w⁽²⁾11 φ1(𝐱) + w⁽²⁾12 φ2(𝐱) + ...w⁽²⁾1M φM(𝐱)) = softmax(𝐰⁽²⁾1ᵀΦ(𝐱)) = exp(a1)/Σj=1:K exp(aj), ai = 𝐰iᵀΦ(𝐱)
>
>
>
> y2 = σ(w⁽²⁾21 φ1(𝐱) + w⁽²⁾22 φ2(𝐱) + ...w⁽²⁾2M φM(𝐱)) = softmax(𝐰⁽²⁾2ᵀΦ(𝐱))
>
>
>
> ...
>
>
>
> φ1(𝐰⁽¹⁾1,𝐱) = h(w⁽¹⁾11x1 + w⁽¹⁾12x2 + ..w⁽¹⁾1DxD + w⁽¹⁾10) = h(a1) = z1 (hidden unit)
>
>
>
> φ2(𝐰⁽¹⁾2,𝐱) =  h(w⁽¹⁾21x1 + w⁽¹⁾22x2 + ..w⁽¹⁾2DxD + w⁽¹⁾20) = h(a2) = z2
>
>
>
> ..
>
>
>
> φM(𝐰⁽¹⁾M,𝐱) =  h(w⁽¹⁾M1x1 + w⁽¹⁾M2x2 + ..w⁽¹⁾MDxD + w⁽¹⁾20)= h(aK) = zK
>
>
>
> ---
>
>
>
>
>
> Vậy qua chương này mục tiêu ở đây sẽ là: Ta tham số hóa hàm basis, ko còn dùng fixed basis function nữa, mà thay nó bằng function có tham số, và tham số này sẽ cũng được xác định (bằng Maximum Likelihood framework giống như tham số đã có)
>
>
>
> Thế thì câu này quan trọng nè: Neural network dùng hàm basis có dạng cũng là non-linear activation function áp lên một hàm tuyến tính của tham số và feature gốc (x1,x2,...).
>
>
>
> ---
>
>
>
> Basic neural network như sau:
>
>
>
> Bước mô tả việc tạo basis function:
>
>
>
> aj = Σi=1:D w⁽¹⁾ji xi + w⁽¹⁾j0, j = 1,2...M, gọi là activations
>
>
>
> zj = h(aj), với h là hàm non-linear activation function, thường dùng sigmoid hay tanh
>
>
>
> Đám z1,...zM (gọi là hidden unit) có thể thấy chính là tương ứng với M basis function φ1(𝐱), φ2(𝐱),...φM(𝐱)
>
>
>
> ---
>
>
>
> Có basis function tiếp theo là như cũ: tạo mô hình y(𝐱) = f(w1 φ1(𝐱) + w2 φ2(𝐱) + .. + w0)
>
>
>
> ak = Σj=1:M w⁽²⁾kj zj + w⁽²⁾k0, gọi là output unit activations
>
>
>
> yk = f(ak)
>
>
>
> Và y như đã nói, với regression f ta dùng hàm identity: yk = ak
>
>
>
> (tác giả không nói nhưng tự hiểu, số output có thể là 1, cho case dự đoán scalar target variable t từ input 𝐱 giống như chapter 3, hoặc cũng có thể cho k &gt; 1 nếu mô hình dự đoán ra vector 𝐭 từ 𝐱)
>
>
>
> với binary classification, ta dùng sigmoid: yk = σ(ak)
>
>
>
> với multiple-class classification, ta dùng softmax transformation: yk = exp(ak) / \[Σs=1:K exp(as)\]
>
>
>
> Như vậy có thể thấy, trước đây mình biết về neural network mình chưa được nghe nói bản chất của cái hidden layer này chính là lớp tạo ra basis function.
>
>
>
> ---
>
>
>
> Như vậy ta có:
>
>
>
> yk(𝐱, 𝐰) = f(Σj=1:M w⁽²⁾kj (h(Σi=1:D w⁽¹⁾ji xi + w⁽¹⁾j0)) + w⁽²⁾k0)
>
>
>
> để rồi neural network về bản chất là hàm phi tuyến giữa input x1,..xD và set các output {y1,y2,...} với sự kiểm soát của vector tham số 𝐰 điều chỉnh được (sẽ được learn từ data)

📹 [Xem video trên YouTube](https://www.youtube.com/watch?v=t2-pF0WzwD0)

> [!TIP]
> 🤖 **AI Check** — 🟡 Minor issues — ✅ **92/100** · ✓ Move on
>
> Ghi chú rất tốt, thể hiện sự hiểu biết sâu sắc và liền mạch từ các mô hình tuyến tính ở Chương 3, 4 sang Neural Network ở Chương 5. Bạn nắm bắt chuẩn xác bản chất: tầng ẩn thực chất là việc học các hàm cơ sở (basis functions) có tham số thay vì cố định.
>
> **🟡 Minor issues**
>
> **1.** *"y1 = σ(w⁽²⁾11 φ1(𝐱) + w⁽²⁾12 φ2(𝐱) + ...w⁽²⁾1M φM(𝐱)) = softmax(𝐰⁽²⁾1ᵀΦ(𝐱))"*
>
> Ký hiệu σ thường dành riêng cho logistic sigmoid (hàm đơn biến). Softmax là hàm đa biến nhận toàn bộ vector activations (a1,..., aK) làm đầu vào; việc viết σ(...) = softmax(...) gây nhập nhằng ký hiệu dù công thức phân thức exp phía sau bạn viết đúng.
>
> **2.** *"φM(𝐰⁽¹⁾M,𝐱) = h(w⁽¹⁾M1x1 + w⁽¹⁾M2x2 + ..w⁽¹⁾MDxD + w⁽¹⁾20)= h(aK) = zK"*
>
> Lỗi gõ nhầm chỉ số: bias phải là w⁽¹⁾M0 (không phải w⁽¹⁾20) và kết quả là h(aM) = zM thay vì h(aK) = zK, vì M là số lượng hidden units còn K là số lượng output units.
>
>
> **✓ Strengths**
> - Liên kết xuất sắc góc nhìn thống kê từ Chương 3 và 4 (tính tuyến tính theo tham số w vs phi tuyến theo x, liên hệ tới Casella-Berger).
> - Nắm bắt chính xác insight cốt lõi của Feed-forward NN: tầng ẩn chính là quá trình tham số hóa và tự thích nghi các basis functions thay cho fixed basis functions.
> - Tổng hợp đầy đủ và chính xác công thức tổng quát yk(x, w) cho mạng 2 lớp (1 hidden layer).
>
> **💡 Deeper notes**
> - Sách PRML phân biệt rõ giữa 'activation' (aj, ak - tổng tuyến tính trước phi tuyến) và 'activation function' h(.) / f(.), bạn đã lưu ý đúng thuật ngữ này.
> - Trong bài toán multiple binary classification (nhiều nhãn nhị phân độc lập), output layer dùng nhiều hàm sigmoid độc lập; còn multiclass (1 trong K lớp) mới dùng softmax liên kết tất cả output units.

<br>

<a id="node-fum466c"></a>

### Figure 5.1 Two-Layer Neural Network

<p align="center"><kbd><img src="assets/xhpkynmrxng.png" width="80%"></kbd></p>

<p align="center"><kbd><img src="assets/xxwcvqf2gx.png" width="80%"></kbd></p>

> [!NOTE]
> Một lưu ý là hình 5.1 không thể hiện probabilistic graphical model (chapter 8 sẽ học)

> [!TIP]
> 🤖 **AI Check** — 🟢 Pass — ✅ **90/100** · ✓ Move on
>
> Ghi chú ngắn gọn và chính xác lưu ý quan trọng trong sách về việc không nhầm lẫn sơ đồ mạng nơ-ron với mô hình đồ thị xác suất.
>
> **✓ Strengths**
> - Nắm bắt chính xác cảnh báo quan trọng trong tài liệu về việc sơ đồ mạng ở Hình 5.1 không phải là mô hình đồ thị xác suất (probabilistic graphical model).
>
> **💡 Deeper notes**
> - Để hiểu sâu hơn, nguyên nhân cốt lõi khiến đây không phải là mô hình đồ thị xác suất là vì các nút bên trong (internal nodes) đại diện cho các biến tiền định (deterministic variables) thay vì các biến ngẫu nhiên (stochastic variables).

<br>

<a id="node-ulxmich"></a>

#### Multilayer Perceptron Network Function

<p align="center"><kbd><img src="assets/lkwefmqt6.png" width="80%"></kbd></p>

> [!NOTE]
> yk(𝐱, 𝐰) = f(Σj=1:M w⁽²⁾kj (h(Σi=1:D w⁽¹⁾ji xi + w⁽¹⁾j0)) + w⁽²⁾k0
>
>
>
> Đoạn này không có gì, chỉ là ta có thể nhập w0 vào luôn bằng cách coi như x0 = 1:
>
>
>
> Σi=1:D w⁽¹⁾ji xi + w⁽¹⁾j0 = Σi=0:D w⁽¹⁾ji xi
>
>
>
> f(Σj=1:M w⁽²⁾kj (h(Σi=0:D w⁽¹⁾ji xi)) + w⁽²⁾k0
>
>
>
> Tương tự coi z0 = 1
>
>
>
> f(Σj=0:M w⁽²⁾kj (h(Σi=0:D w⁽¹⁾ji xi))
>
>
>
> Và từ đó nó giống như hai layer mà mỗi layer là perceptron. nên người ta gọi là multi layer perceptron
>
>
>
> Nhưng điểm khác biệt chính là ở đây xài hàm activation function phi tuyến liên tục, chứ ko phải step function, nên nó có tính defferentiable nên có thể dùng đạo hàm để learn param được.

> [!TIP]
> 🤖 **AI Check** — 🟡 Minor issues — ✅ **95/100** · ✓ Move on
>
> Ghi chú nắm rất chắc và chính xác bản chất việc hấp thụ bias vào trọng số cũng như sự khác biệt cốt lõi giữa MLP và perceptron cổ điển.
>
> **🟡 Minor issues**
>
> **1.** *"f(Σj=0:M w⁽²⁾kj (h(Σi=0:D w⁽¹⁾ji xi))"*
>
> Biểu thức thiếu một dấu ngoặc đóng cho hàm kích hoạt ngoài cùng `f(...)`. Ngoài ra, về mặt ký hiệu hình thức, khi $j=0$ thì $z_0 = 1$ là một giá trị gán trực tiếp (clamped) chứ không nhất thiết phải tính qua hàm kích hoạt $h(\cdot)$ từ tầng trước.
>
>
> **✓ Strengths**
> - Hiểu chính xác cơ chế gộp bias $w_0$ vào ma trận trọng số bằng cách bổ sung biến giả $x_0 = 1$ và $z_0 = 1$.
> - Nắm vững lý do mạng nơ-ron được gọi là MLP và phân biệt rõ vai trò của hàm kích hoạt phi tuyến liên tục (differentiable) so với step function trong việc tối ưu bằng gradient.
>
> **💡 Deeper notes**
> - Trong công thức (5.9) của sách Bishop, việc viết $h(\sum_{i=0}^D w_{ji}^{(1)} x_i)$ chạy từ $j=0$ là một dạng lạm dụng ký hiệu gọn; trên thực tế $z_0 = 1$ được định nghĩa độc lập để tạo ra bias $w_{k0}^{(2)}$ cho lớp thứ hai.

<br>

<a id="node-uzyru4g"></a>

##### Networks of Linear Hidden Units

<p align="center"><kbd><img src="assets/uuyi97lcrdj.png" width="80%"></kbd></p>

> [!NOTE]
> Đại ý là nói nếu hidden unit không dùng activation function, thì network này có thể tương đương một network không có hidden unit. Lí do là các hợp của các linear transformation sẽ cũng tạo linear transformation
>
>
>
> (cái này dễ thấy)
>
>
>
> Ý tiếp, nếu số hidden unit nhỏ hơn số input hay output thì phép biến đổi tuyến tính tạo bỏi cả network sẽ không phải là most general possible linear transformation vì thông tin bị mất do việc giảm chiều của hidden layer.
>
>
>
> Vậy đại ý là nếu số hidden unit nhỏ hơn số input hay output và không xài non-linear activation function của unit layer, cơ bản là ta sẽ có network làm việc như một hàm biến đổi tuyến tính như lại ko có được khả năng thể hiện mọi dạng linear transformation.
>
>
>
> Nên network dùng linear unit hầu như ko có ích lợi gì

> [!TIP]
> 🤖 **AI Check** — 🟢 Pass — ✅ **95/100** · ✓ Move on
>
> Ghi chú tóm tắt rất chính xác và mạch lạc nội dung cốt lõi của đoạn trích về mạng nơ-ron có các tầng ẩn tuyến tính.
>
> **✓ Strengths**
> - Nắm chính xác bản chất toán học: hợp của các phép biến đổi tuyến tính liên tiếp vẫn là một phép biến đổi tuyến tính.
> - Hiểu đúng hệ quả về chiều (rank): khi số hidden units nhỏ hơn input hoặc output thì ma trận biểu diễn bị giới hạn rank, dẫn đến mất thông tin và không thể biểu diễn mọi ánh xạ tuyến tính tổng quát.
> - Tổng hợp và rút ra kết luận thực tế chuẩn xác rằng mạng nhiều tầng tuyến tính nhìn chung không mang lại nhiều giá trị biểu diễn phi tuyến.
>
> **💡 Deeper notes**
> - Về mặt thuật ngữ, 'không dùng activation function' thường ngầm hiểu là hàm đồng nhất (identity), trong khi sách đề cập tổng quát là 'hàm kích hoạt tuyến tính' (linear activation function).
> - Mặc dù nhìn chung ít được ứng dụng thực tế do tính chất tuyến tính, mạng tuyến tính có tầng ẩn thắt nút (bottleneck) vẫn có ý nghĩa lý thuyết quan trọng vì nó liên hệ trực tiếp với phương pháp Phân tích Thành phần Chính (PCA) như sách có đề cập.

<br>

