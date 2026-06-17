# BÀI 2: Tối ưu Prompt (Bảo mật thông tin nhạy cảm)

## Prompt sau khi tối ưu

```text
Hãy viết một class Java tên VNPayPaymentService để hỗ trợ tích hợp thanh toán VNPay. Yêu cầu tuyệt đối không hardcode API Key, Hash Secret hoặc bất kỳ thông tin nhạy cảm nào trong mã nguồn. Hãy sử dụng System.getenv() để đọc khóa bí mật từ biến môi trường có tên VNPAY_HASH_SECRET.

Ngoài ra, hãy bổ sung cơ chế kiểm tra an toàn: nếu biến môi trường không tồn tại, bằng null hoặc chuỗi rỗng thì phải ném ra IllegalStateException với thông báo rõ ràng. Trả về mã nguồn Java hoàn chỉnh và tuân thủ các nguyên tắc bảo mật khi triển khai hệ thống thanh toán.
```

## Mã nguồn Java an toàn do AI sinh ra

```java
public class VNPayPaymentService {

    private static final String VNP_URL =
            "https://sandbox.vnpayment.vn/paymentv2/vpcpay.html";

    private final String hashSecret;

    public VNPayPaymentService() {
        this.hashSecret = loadHashSecret();
    }

    private String loadHashSecret() {
        String secret = System.getenv("VNPAY_HASH_SECRET");

        if (secret == null || secret.trim().isEmpty()) {
            throw new IllegalStateException(
                "Biến môi trường VNPAY_HASH_SECRET chưa được cấu hình."
            );
        }

        return secret;
    }

    public String createPayment(long amount, String orderId) {

        // Ví dụ minh họa tạo thông tin thanh toán
        StringBuilder paymentInfo = new StringBuilder();

        paymentInfo.append("VNPay URL: ")
                   .append(VNP_URL)
                   .append("\nOrder ID: ")
                   .append(orderId)
                   .append("\nAmount: ")
                   .append(amount);

        // Thực tế sẽ sử dụng hashSecret để ký dữ liệu giao dịch
        // trước khi gửi tới VNPay.

        return paymentInfo.toString();
    }

    public String getHashSecret() {
        return hashSecret;
    }
}
```
