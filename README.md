<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Cửa Hàng Trực Tuyến</title>
    <style>
        /* Cài đặt cơ bản */
        * { box-sizing: border-box; margin: 0; padding: 0; font-family: Arial, sans-serif; }
        body { background-color: #f5f5f5; color: #333; }

        /* Thanh điều hướng (Header) phong cách Shopee */
        header {
            background-color: #ee4d2d;
            padding: 15px 20px;
            color: white;
            display: flex;
            justify-content: space-between;
            align-items: center;
            position: sticky;
            top: 0;
            z-index: 100;
        }
        header h1 { font-size: 24px; }
        .search-bar { padding: 8px; border: none; border-radius: 2px; width: 300px; }

        /* Khu vực danh sách sản phẩm */
        .container { max-width: 1200px; margin: 20px auto; padding: 0 10px; }
        .product-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
            gap: 15px;
        }

        /* Thẻ Sản Phẩm */
        .product-card {
            background: white;
            border-radius: 3px;
            overflow: hidden;
            box-shadow: 0 1px 2px rgba(0,0,0,0.1);
            transition: transform 0.2s, box-shadow 0.2s;
            cursor: pointer;
        }
        .product-card:hover {
            transform: translateY(-2px);
            box-shadow: 0 4px 8px rgba(0,0,0,0.2);
        }
        .product-img { width: 100%; height: 200px; object-fit: cover; }
        .product-info { padding: 10px; }
        .product-title {
            font-size: 14px;
            margin-bottom: 8px;
            display: -webkit-box;
            -webkit-line-clamp: 2;
            -webkit-box-orient: vertical;
            overflow: hidden;
            text-overflow: ellipsis;
        }
        .product-price { color: #ee4d2d; font-size: 16px; font-weight: bold; }

        /* Cửa sổ chi tiết sản phẩm (Modal) */
        .modal {
            display: none; 
            position: fixed; 
            z-index: 1000; 
            left: 0; top: 0; 
            width: 100%; height: 100%; 
            background-color: rgba(0,0,0,0.5);
        }
        .modal-content {
            background-color: #fff;
            margin: 5% auto;
            padding: 20px;
            width: 90%;
            max-width: 800px;
            border-radius: 5px;
            position: relative;
            display: flex;
            flex-direction: column;
            gap: 20px;
            max-height: 80vh;
            overflow-y: auto;
        }
        .close-btn {
            position: absolute;
            top: 10px; right: 15px;
            font-size: 28px;
            font-weight: bold;
            color: #aaa;
            cursor: pointer;
        }
        .close-btn:hover { color: #333; }

        /* Bố cục bên trong Modal */
        .modal-body { display: flex; gap: 20px; flex-wrap: wrap; }
        .modal-image { flex: 1; min-width: 250px; }
        .modal-image img { width: 100%; border-radius: 5px; }
        .modal-details { flex: 2; min-width: 300px; }
        .modal-details h2 { font-size: 20px; margin-bottom: 10px; }
        .modal-details .price { color: #ee4d2d; font-size: 24px; font-weight: bold; margin-bottom: 15px; }
        .modal-details p { line-height: 1.5; margin-bottom: 20px; color: #555; }
        .buy-btn {
            background-color: #ee4d2d; color: white;
            border: none; padding: 10px 20px; font-size: 16px;
            cursor: pointer; border-radius: 3px; width: 100%;
        }
        .buy-btn:hover { background-color: #d73a1e; }

        /* Phần Bình Luận */
        .comments-section { margin-top: 20px; border-top: 1px solid #eee; padding-top: 15px; }
        .comment { margin-bottom: 15px; }
        .comment-author { font-weight: bold; margin-bottom: 5px; font-size: 14px;}
        .comment-text { font-size: 14px; color: #444; background: #f9f9f9; padding: 10px; border-radius: 5px;}
    </style>
</head>
<body>

    <header>
        <h1>MyStore</h1>
        <input type="text" class="search-bar" placeholder="Tìm kiếm sản phẩm...">
    </header>

    <div class="container">
        <div class="product-grid">
            
            <!-- SẢN PHẨM 1 -->
            <!-- Để thay đổi thông tin, hãy sửa các dòng 'data-...' ở thẻ div bên dưới -->
            <div class="product-card" onclick="openModal(this)"
                 data-title="Áo Thun Nam Cổ Tròn Thun Cotton Cao Cấp" 
                 data-price="₫150.000"
                 data-desc="Áo thun nam chất liệu cotton 100%, co giãn 4 chiều, thấm hút mồ hôi tốt. Phù hợp mặc đi chơi, đi làm."
                 data-image="https://images.unsplash.com/photo-1521572163474-6864f9cf17ab?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60">
                <!-- THAY ĐỔI ẢNH HIỂN THỊ TẠI ĐÂY (Sửa đường dẫn trong src="") -->
                <img src="https://images.unsplash.com/photo-1521572163474-6864f9cf17ab?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60" alt="Áo Thun" class="product-img">
                <div class="product-info">
                    <!-- THAY ĐỔI TÊN SẢN PHẨM Ở ĐÂY -->
                    <div class="product-title">Áo Thun Nam Cổ Tròn Thun Cotton Cao Cấp</div>
                    <!-- THAY ĐỔI GIÁ SẢN PHẨM Ở ĐÂY -->
                    <div class="product-price">₫150.000</div>
                </div>
            </div>

            <!-- SẢN PHẨM 2 -->
            <div class="product-card" onclick="openModal(this)"
                 data-title="Tai Nghe Không Dây Bluetooth 5.0 Chống Ồn" 
                 data-price="₫299.000"
                 data-desc="Tai nghe không dây âm thanh chất lượng cao, pin sử dụng liên tục 6 tiếng. Thiết kế nhỏ gọn, kèm hộp sạc tiện lợi."
                 data-image="https://images.unsplash.com/photo-1590658268037-6bf12165a8df?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60">
                <img src="https://images.unsplash.com/photo-1590658268037-6bf12165a8df?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60" alt="Tai Nghe" class="product-img">
                <div class="product-info">
                    <div class="product-title">Tai Nghe Không Dây Bluetooth 5.0 Chống Ồn</div>
                    <div class="product-price">₫299.000</div>
                </div>
            </div>

            <!-- SẢN PHẨM 3 -->
            <div class="product-card" onclick="openModal(this)"
                 data-title="Đồng Hồ Nam Dây Da Thể Thao Chống Nước" 
                 data-price="₫450.000"
                 data-desc="Đồng hồ nam phong cách lịch lãm, mặt kính sapphire chống trầy xước, chống nước sinh hoạt 3ATM."
                 data-image="https://images.unsplash.com/photo-1524592094714-0f0654e20314?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60">
                <img src="https://images.unsplash.com/photo-1524592094714-0f0654e20314?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60" alt="Đồng Hồ" class="product-img">
                <div class="product-info">
                    <div class="product-title">Đồng Hồ Nam Dây Da Thể Thao Chống Nước</div>
                    <div class="product-price">₫450.000</div>
                </div>
            </div>

        </div>
    </div>

    <!-- KHU VỰC CỬA SỔ HIỂN THỊ CHI TIẾT (Bị ẩn mặc định) -->
    <div id="productModal" class="modal">
        <div class="modal-content">
            <span class="close-btn" onclick="closeModal()">&times;</span>
            
            <div class="modal-body">
                <div class="modal-image">
                    <img id="modal-img" src="" alt="Hình ảnh sản phẩm">
                </div>
                <div class="modal-details">
                    <h2 id="modal-title">Tên sản phẩm</h2>
                    <div class="price" id="modal-price">₫0</div>
                    <p id="modal-desc">Mô tả sản phẩm sẽ hiện ở đây...</p>
                    <button class="buy-btn">Thêm vào giỏ hàng</button>
                </div>
            </div>

            <!-- Khu vực bình luận mẫu -->
            <div class="comments-section">
                <h3>Đánh giá sản phẩm</h3>
                <div class="comment">
                    <div class="comment-author">Nguyễn Văn A - ⭐⭐⭐⭐⭐</div>
                    <div class="comment-text">Giao hàng rất nhanh, đóng gói cẩn thận. Sản phẩm giống y như mô tả. Sẽ ủng hộ shop dài dài!</div>
                </div>
                <div class="comment">
                    <div class="comment-author">Trần Thị B - ⭐⭐⭐⭐</div>
                    <div class="comment-text">Chất lượng tạm ổn trong tầm giá. Màu sắc thực tế hơi đậm hơn trên hình một chút nhưng vẫn đẹp.</div>
                </div>
            </div>

        </div>
    </div>

    <script>
        // Hàm lấy dữ liệu từ thẻ sản phẩm và đưa vào cửa sổ pop-up (Modal)
        function openModal(element) {
            // Lấy dữ liệu từ các thuộc tính data-... mà bạn thiết lập ở HTML
            const title = element.getAttribute('data-title');
            const price = element.getAttribute('data-price');
            const desc = element.getAttribute('data-desc');
            const imageSrc = element.getAttribute('data-image');

            // Cập nhật thông tin vào Modal
            document.getElementById('modal-title').innerText = title;
            document.getElementById('modal-price').innerText = price;
            document.getElementById('modal-desc').innerText = desc;
            document.getElementById('modal-img').src = imageSrc;

            // Hiển thị Modal
            document.getElementById('productModal').style.display = "block";
        }

        // Hàm đóng cửa sổ pop-up
        function closeModal() {
            document.getElementById('productModal').style.display = "none";
        }

        // Bấm ra ngoài cửa sổ để đóng
        window.onclick = function(event) {
            const modal = document.getElementById('productModal');
            if (event.target == modal) {
                modal.style.display = "none";
            }
        }
    </script>
</body>
</html>
