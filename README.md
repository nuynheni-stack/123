<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>線上商城</title>
    <style>
        /* 基礎網頁樣式 */
        body { font-family: "Microsoft JhengHei", Arial, sans-serif; background-color: #f5f5f5; margin: 0; padding: 20px; }
        header { background-color: #ee4d2d; color: white; padding: 15px; text-align: center; font-size: 24px; font-weight: bold; margin-bottom: 20px; }
        
        /* 商品列表排版 */
        .product-grid { display: flex; gap: 20px; justify-content: center; flex-wrap: wrap; }
        
        /* 商品卡片樣式 */
        .product-card { background: white; border: 1px solid #ddd; width: 220px; padding: 10px; border-radius: 4px; cursor: pointer; }
        .product-card img { width: 100%; height: 200px; object-fit: cover; }
        .product-title { font-size: 14px; margin: 10px 0; height: 40px; overflow: hidden; }
        .product-price { color: #ee4d2d; font-size: 16px; font-weight: bold; }

        /* 彈出視窗樣式（預設隱藏） */
        .modal { display: none; position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.6); z-index: 100; }
        .modal-content { background: white; width: 500px; margin: 10% auto; padding: 20px; border-radius: 5px; position: relative; }
        .close-btn { position: absolute; top: 10px; right: 15px; font-size: 24px; cursor: pointer; color: #aaa; }
        .close-btn:hover { color: #ee4d2d; }
        
        /* 彈出視窗內部詳細資訊 */
        #modal-img { width: 100%; max-height: 300px; object-fit: cover; }
        #modal-price { color: #ee4d2d; font-size: 22px; font-weight: bold; margin: 10px 0; }
        #modal-desc { color: #666; margin-bottom: 20px; line-height: 1.5; font-size: 14px; }
        
        /* 評論區塊樣式 */
        .comments { border-top: 1px solid #eee; padding-top: 15px; }
        .comment-item { background: #f9f9f9; padding: 8px; margin-bottom: 8px; border-radius: 4px; font-size: 13px; }
    </style>
</head>
<body>

    <!-- 頂部導覽列 -->
    <header>蝦皮風線上商城</header>

    <!-- 商品展示區域 -->
    <div class="product-grid">

        <!-- === 商品 1 === -->
        <div class="product-card" onclick="showProduct('男士純棉短袖T恤', 'NT$ 350', 'https://picsum.photos/id/26/500/500', '這款短袖T恤採用100%純棉材質製成，吸汗透氣性極佳，剪裁舒適，非常適合日常休閒與通勤穿著。')">
            <img src="https://picsum.photos/id/26/500/500" alt="商品1">
            <div class="product-title">男士純棉短袖T恤</div>
            <div class="product-price">NT$ 350</div>
        </div>

        <!-- === 商品 2 === -->
        <div class="product-card" onclick="showProduct('無線藍牙降噪耳機', 'NT$ 890', 'https://picsum.photos/id/48/500/500', '最新藍牙5.0技術，支援主動降噪功能，音質清晰純淨。單次充電可連續使用6小時，搭配充電盒續航長達24小時。')">
            <img src="https://picsum.photos/id/48/500/500" alt="商品2">
            <div class="product-title">無線藍牙降噪耳機</div>
            <div class="product-price">NT$ 890</div>
        </div>

        <!-- === 商品 3 === -->
        <div class="product-card" onclick="showProduct('運動防水真皮手錶', 'NT$ 1,250', 'https://picsum.photos/id/175/500/500', '精選真皮錶帶，展現優雅商務風範。內建30米生活防水功能，鏡面採用高硬度防刮玻璃，耐磨且持久。')">
            <img src="https://picsum.photos/id/175/500/500" alt="商品3">
            <div class="product-title">運動防水真皮手錶</div>
            <div class="product-price">NT$ 1,250</div>
        </div>

    </div>

    <!-- 商品詳細資訊彈出視窗 (Modal) -->
    <div id="productModal" class="modal">
        <div class="modal-content">
            <span class="close-btn" onclick="closeModal()">&times;</span>
            <img id="modal-img" src="" alt="商品圖片">
            <h2 id="modal-title">商品名稱</h2>
            <div id="modal-price">NT$ 0</div>
            <p id="modal-desc">這裡顯示詳細介紹...</p>
            
            <!-- 買家評論區塊 -->
            <div class="comments">
                <h3>商品評價（買家留言）</h3>
                <div class="comment-item"><b>王*明 (⭐⭐⭐⭐⭐):</b> 商品質感非常好，出貨速度超快！非常滿意！</div>
                <div class="comment-item"><b>陳*美 (⭐⭐⭐⭐):</b> 包裝完整沒有缺損，實品跟照片一樣，CP值很高。</div>
            </div>
        </div>
    </div>

    <script>
        // 點擊商品卡片時觸發的函式（將資料帶入彈出視窗並顯示）
        function showProduct(name, price, imgUrl, description) {
            document.getElementById('modal-title').innerText = name;
            document.getElementById('modal-price').innerText = price;
            document.getElementById('modal-img').src = imgUrl;
            document.getElementById('modal-desc').innerText = description;
            
            document.getElementById('productModal').style.display = "block";
        }

        // 關閉彈出視窗的函式
        function closeModal() {
            document.getElementById('productModal').style.display = "none";
        }

        // 點擊彈出視窗以外的灰色區域時自動關閉
        window.onclick = function(event) {
            var modal = document.getElementById('productModal');
            if (event.target == modal) {
                modal.style.display = "none";
            }
        }
    </script>

</body>
</html>
