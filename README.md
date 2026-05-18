<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>線上商城</title>
    <style>
        /* Giao diện cơ bản kiểu Shopee */
        body { font-family: Arial, sans-serif; background-color: #f5f5f5; margin: 0; padding: 20px; }
        header { background-color: #ee4d2d; color: white; padding: 15px; text-align: center; font-size: 24px; font-weight: bold; margin-bottom: 20px; }
        
        /* Bố cục danh sách sản phẩm */
        .product-grid { display: flex; gap: 20px; justify-content: center; flex-wrap: wrap; }
        
        /* Thẻ sản phẩm */
        .product-card { background: white; border: 1px solid #ddd; width: 220px; padding: 10px; border-radius: 4px; cursor: pointer; }
        .product-card img { width: 100%; height: 200px; object-fit: cover; }
        .product-title { font-size: 14px; margin: 10px 0; height: 40px; overflow: hidden; }
        .product-price { color: #ee4d2d; font-size: 16px; font-weight: bold; }

        /* Cửa sổ chi tiết sản phẩm (Mặc định là ẩn) */
        .modal { display: none; position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.6); z-index: 100; }
        .modal-content { background: white; width: 500px; margin: 10% auto; padding: 20px; border-radius: 5px; position: relative; }
        .close-btn { position: absolute; top: 10px; right: 15px; font-size: 24px; cursor: pointer; color: #aaa; }
        .close-btn:hover { color: #ee4d2d; }
        
        /* Chi tiết trong bảng popup */
        #modal-img { width: 100%; max-height: 300px; object-fit: cover; }
        #modal-price { color: #ee4d2d; font-size: 22px; font-weight: bold; margin: 10px 0; }
        #modal-desc { color: #666; margin-bottom: 20px; line-height: 1.5; }
        
        /* Phần bình luận */
        .comments { border-top: 1px solid #eee; padding-top: 15px; }
        .comment-item { background: #f9f9f9; padding: 8px; margin-bottom: 8px; border-radius: 4px; font-size: 13px; }
    </style>
</head>
<body>

    <header>線上商城</header>

    <div class="product-grid">

        <!-- === SẢN PHẨM 1 === -->
        <div class="product-card" onclick="showProduct('男士純棉短袖T恤', 'NT$ 350', 'https://picsum.photos/id/26/500/500', '這 b0 是 100% 純棉材質的短袖T恤，吸汗透氣，穿著非常舒適。')">
            <img src="https://picsum.photos/id/26/500/500" alt="商品1">
            <div class="product-title">男士純棉短袖T恤</div>
            <div class="product-price">NT$ 350</div>
        </div>

        <!-- === SẢN PHẨM 2 === -->
        <div class="product-card" onclick="showProduct('無線藍牙降噪耳機', 'NT$ 890', 'https://picsum.photos/id/48/500/500', '這款藍牙耳機支援主動降噪，音質清晰，續航力長達24小時。')">
            <img src="https://picsum.photos/id/48/500/500" alt="商品2">
            <div class="product-title">無線藍牙降噪耳機</div>
            <div class="product-price">NT$ 890</div>
        </div>

        <!-- === SẢN PHẨM 3 === -->
        <div class="product-card" onclick="showProduct('運動防水真皮手錶', 'NT$ 1,250', 'https://picsum.photos/id/175/500/500', '真皮錶帶商務手錶，支援30米生活防水，鏡面防刮耐磨。')">
            <img src="https://picsum.photos/id/175/500/500" alt="商品3">
            <div class="product-title">運動防水真皮手錶</div>
            <div class="product-price">NT$ 1,250</div>
        </div>

    </div>

    <!-- CỬA SỔ POPUP CHI TIẾT SẢN PHẨM -->
    <div id="productModal" class="modal">
        <div class="modal-content">
            <span class="close-btn" onclick="closeModal()">&times;</span>
            <img id="modal-img" src="" alt="商品圖片">
            <h2 id="modal-title">商品名稱</h2>
            <div id="modal-price">NT$ 0</div>
            <p id="modal-desc">這裡顯示詳細介紹...</p>
            
            <!-- Khu vực bình luận cố định -->
            <div class="comments">
                <h3>商品評價 (買家評論)</h3>
                <div class="comment-item"><b>王**明 (⭐⭐⭐⭐⭐):</b> 東西很好看，出貨速度也很快！</div>
                <div class="comment-item"><b>陳**美 (⭐⭐⭐⭐):</b> 品質還可以，包裝得很完整。</div>
            </div>
        </div>
    </div>

    <script>
        // Hàm mở cửa sổ chi tiết khi bấm vào sản phẩm
        function showProduct(name, price, imgUrl, description) {
            document.getElementById('modal-title').innerText = name;
            document.getElementById('modal-price').innerText = price;
            document.getElementById('modal-img').src = imgUrl;
            document.getElementById('modal-desc').innerText = description;
            
            document.getElementById('productModal').style.display = "block";
        }

        // Hàm đóng cửa sổ
        function closeModal() {
            document.getElementById('productModal').style.display = "none";
        }

        // Bấm ra ngoài vùng trắng để đóng cửa sổ
        window.onclick = function(event) {
            var modal = document.getElementById('productModal');
            if (event.target == modal) {
                modal.style.display = "none";
            }
        }
    </script>

</body>
</html>
