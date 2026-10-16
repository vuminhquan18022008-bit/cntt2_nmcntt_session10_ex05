# Phần 1 : phân tích 
## 1.1 xác định INPUT , OUTPUT 
- **Input( đầu vào )** : Dữ liệu từ cảm biến và yêu cầu của người dùng
- **Process** (Xử lý):	Vi điều khiển đọc dữ liệu, so sánh ngưỡng và quyết định tưới	Nhiệt độ cao, đất khô
- **Output (Đầu ra)**	: Lệnh điều khiển thiết bị và thông tin hiển thị

## 1.2 Sơ đồ phối hợp phần cứng 

*Cảm biến Iot ===>Vi điều khiển===>Máy bơm Van===>Bảng điều khiển*

# Phần 2 : Triển khai 


## 🚀 Smart-Farm -- Hệ thống tưới tiêu thông minh
**1. Giới thiệu dự án**
Smart-Farm là hệ thống ứng dụng Internet of Things (IoT) để hỗ trợ
người nông dân tại trang trại Lan giám sát môi trường, theo dõi tình
trạng cây trồng và điều khiển thiết bị tưới
**2. Cách thức vận hành của hệ thống**
- Cảm biến : thu thập dữ liệu ( nhiệt độ , độ ẩm )
- Gateway : Gửi dữ liệu lên internet
- nền tảng : lưu trữ và xử lí dữ liệu
- ứng dụng : hiển thị và báo cáo
- thiết bị điều khiển tự động

**3.Các bước sử dụng :**
1. đăng nhập vào ứng dụng Smart-Farm
   - Mở ứng dụng Smart-farm
   - nhập tài khoản  và mật khẩu 
2. xem thông số môi trường
   - xem các thông số theo thời gian thực
   - màu sắc giúp nhận biết nhanh tình trạng
3. nhận cảnh báo
   - kiểm tra và xử lí kịp thời
4. Điều khiển thiết bị
   - chọn chế độ tự động
5. xem báo cáo
   - xem lịch sử theo ngày tuần

**4. Bảng thông số**
| Thông số | Giá trị hiển thị trong hình | Ý nghĩa |
|---|---|---|
| Nhiệt độ | 28.6 °C | Nhiệt độ môi trường |
| Độ ẩm không khí | 78% | Độ ẩm tương đối của không khí |
| Độ ẩm đất | 65% | Giá trị từ cảm biến độ ẩm đất |
| Ánh sáng | 1200 lux | Mức độ chiếu sáng |
| EC | 1.6 mS/cm | Độ dẫn điện của dung dịch hoặc môi trường đo |
| pH | 6.2 | Chỉ số độ axit/kiềm |

## Chức năng 2: Mô tả chu kỳ Fetch–Decode–Execute

CPU (Central Processing Unit – Bộ xử lý trung tâm) thực hiện chu kỳ Fetch–Decode–Execute để nạp, giải mã và thực thi lệnh. Trong hệ thống Smart-Farm IoT, chu kỳ này được minh họa qua việc xử lý lệnh tưới nước cho cây lan.

> **Bước 1 – Fetch (Nạp lệnh):** CPU lấy lệnh `TURN_ON_PUMP` từ chương trình điều khiển.
>
> **Bước 2 – Decode (Giải mã lệnh):** CPU giải mã lệnh để xác định yêu cầu bật máy bơm. Bộ điều khiển kiểm tra dữ liệu cảm biến và các điều kiện an toàn trước khi cho phép tưới.
>
> **Bước 3 – Execute (Thực thi lệnh):** Nếu điều kiện tưới hợp lệ, bộ điều khiển gửi tín hiệu đến mạch điều khiển để bật máy bơm hoặc van nước. Sau đó, hệ thống tiếp tục theo dõi cảm biến để kiểm tra trạng thái hoạt động.

**Ý nghĩa:** Chu kỳ Fetch–Decode–Execute mô tả cách CPU xử lý lệnh. CPU không trực tiếp cấp điện cho máy bơm; thiết bị chấp hành được điều khiển thông qua bộ điều khiển và mạch công suất phù hợp.

---

## Chức năng 3: DIKW – Chuyển hóa dữ liệu nhiệt độ thành hành động tưới

DIKW là mô hình gồm bốn cấp độ: **Data (Dữ liệu), Information (Thông tin), Knowledge (Tri thức) và Wisdom (Sự khôn ngoan)**. Trong hệ thống Smart-Farm IoT, mô hình này thể hiện quá trình chuyển đổi dữ liệu nhiệt độ thành quyết định chăm sóc cây lan.

### 3.1. Mô hình kim tự tháp DIKW

```text
                  /\
                 /  \
                / W  \          WISDOM
               /______\         Quyết định tưới phù hợp
              /        \
             /    K     \       KNOWLEDGE
            /____________\      Áp dụng quy tắc chăm sóc
           /              \
          /       I        \    INFORMATION
         /__________________\   Phân tích nhiệt độ
        /                    \
       /          D           \ DATA
      /________________________\ Giá trị cảm biến



## Lưu ý (Notes): Xử lý an toàn khi RAM đầy dữ liệu nhật ký

Khi bộ nhớ RAM bị đầy do dữ liệu nhật ký (log), hệ thống Smart-Farm IoT có thể hoạt động chậm, mất dữ liệu tạm thời hoặc ngừng phản hồi. Cần thực hiện các biện pháp xử lý an toàn sau:



### Nguyên tắc an toàn

- Không tắt hoặc khởi động lại hệ thống một cách tùy tiện khi máy bơm đang hoạt động.
- Không để dữ liệu nhật ký chiếm toàn bộ RAM; cần có cơ chế giới hạn và giám sát bộ nhớ.
- Không tự động bật lại máy bơm nếu chưa xác nhận các điều kiện tưới an toàn.
- Ưu tiên bảo đảm an toàn cho cây trồng và thiết bị trước khi khôi phục hoạt động bình thường.
