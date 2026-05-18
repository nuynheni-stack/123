<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>線上商城</title>
    <style>
        /* 基本設定 */
        * { box-sizing: border-box; margin: 0; padding: 0; font-family: 'PingFang TC', 'Microsoft JhengHei', sans-serif; }
        body { background-color: #f5f5f5; color: #333; }

        /* 導覽列 (Header) */
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
        header h1 { font-size: 24px; letter-spacing: 1px; }
        .search-bar { padding: 8px 15px; border: none; border-radius: 2px; width: 300px; outline: none; }

        /* 商品區塊 */
        .container { max-width: 1200px; margin: 20px auto; padding: 0 10px; }
        .product-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
            gap: 15px;
        }

        /* 商品卡片 */
        .product-card {
            background: white;
            border-radius: 3px;
            overflow: hidden;
            box-shadow: 0 1px 2px rgba(0,0,0,0.1);
            transition: transform 0.2s, box-shadow 0.2s;
            cursor: pointer;
            display: flex;
            flex-direction: column;
        }
        .product-card:hover {
            transform: translateY(-2px);
            box-shadow: 0 4px 8px rgba(0,0,0,0.2);
        }
        .product-img { width: 100%; height: 200px; object-fit: cover; }
        .product-info { padding: 10px; display: flex; flex-direction: column; justify-content: space-between; flex-grow: 1; }
        .product-title {
            font-size: 14px;
            margin-bottom: 8px;
            display: -webkit-box;
            -webkit-line-clamp: 2;
            -webkit-box-orient: vertical;
            overflow: hidden;
            text-overflow: ellipsis;
            line-height: 1.4;
        }
        .product-price { color: #ee4d2d; font-size: 16px; font-weight: bold; margin-top: auto; }

        /* 彈出視窗 (Modal) */
        .modal {
            display: none; 
            position: fixed; 
            z-index: 1000; 
            left: 0; top: 0; 
            width: 100%; height: 100%; 
            background-color: rgba(0,0,0,0.6);
        }
        .modal-content {
            background-color: #fff;
            margin: 5vh auto;
            padding: 25px;
            width: 90%;
            max-width: 800px;
            border-radius: 5px;
            position: relative;
            display: flex;
            flex-direction: column;
            gap: 20px;
            max-height: 90vh;
            overflow-y: auto;
        }
        .close-btn {
            position: absolute;
            top: 10px; right: 20px;
            font-size: 30px;
            font-weight: bold;
            color: #aaa;
            cursor: pointer;
            transition: color 0.2s;
        }
        .close-btn:hover { color: #ee4d2d; }

        /* 彈出視窗內容佈局 */
        .modal-body { display: flex; gap: 25px; flex-wrap: wrap; }
        .modal-image { flex: 1; min-width: 250px; }
        .modal-image img { width: 100%; border-radius: 5px; object-fit: cover; }
        .modal-details { flex: 1.5; min-width: 300px; display: flex; flex-direction: column; }
        .modal-details h2 { font-size: 22px; margin-bottom: 15px; line-height: 1.4; }
        .modal-details .price { color: #ee4d2d; font-size: 26px; font-weight: bold; margin-bottom: 15px; }
        .modal-details p { line-height: 1.6; margin-bottom: 25px; color: #555; }
        .buy-btn {
            background-color: #ee4d2d; color: white;
            border: none; padding: 12px 20px; font-size: 16px;
            cursor: pointer; border-radius: 3px; width: 100%;
            margin-top: auto; transition: background 0.2s;
        }
        .buy-btn:hover { background-color: #d73a1e; }

        /* 評價區塊 */
        .comments-section { margin-top: 20px; border-top: 1px solid #eee; padding-top: 20px; }
        .comments-section h3 { font-size: 18px; margin-bottom: 15px; }
        .comment { margin-bottom: 15px; background: #fdfdfd; padding: 12px; border-radius: 5px; border: 1px solid #f0f0f0; }
        .comment-author { font-weight: bold; margin-bottom: 8px; font-size: 14px; color: #333; }
        .comment-text { font-size: 14px; color: #666; line-height: 1.5; }
    </style>
</head>
<body>

    <header>
        <h1>線上商城</h1>
        <input type="text" class="search-bar" placeholder="搜尋商品...">
    </header>

    <div class="container">
        <!-- Danh sách sản phẩm sẽ được tạo tự động tại đây -->
        <div class="product-grid" id="productGrid"></div>
    </div>

    <!-- 彈出視窗 (Cửa sổ chi tiết) -->
    <div id="productModal" class="modal">
        <div class="modal-content">
            <span class="close-btn" onclick="closeModal()">&times;</span>
            
            <div class="modal-body">
                <div class="modal-image">
                    <img id="modal-img" src="" alt="商品圖片">
                </div>
                <div class="modal-details">
                    <h2 id="modal-title">商品名稱</h2>
                    <div class="price" id="modal-price">NT$ 0</div>
                    <p id="modal-desc">商品描述...</p>
                    <button class="buy-btn">加入購物車</button>
                </div>
            </div>

            <div class="comments-section">
                <h3>商品評價</h3>
                <!-- Bình luận mẫu (Bạn có thể thêm bớt tại đây) -->
                <div class="comment">
                    <div class="comment-author">王小明 - ⭐⭐⭐⭐⭐</div>
                    <div class="comment-text">出貨速度超快，包裝得很仔細。實品跟照片一樣好看，下次還會再回購！</div>
                </div>
                <div class="comment">
                    <div class="comment-author">林美玲 - ⭐⭐⭐⭐</div>
                    <div class="comment-text">CP值很高，材質還不錯。如果顏色能再亮一點就更完美了。</div>
                </div>
            </div>
        </div>
    </div>

    <script>
        // =========================================================
        // KHU VỰC DỮ LIỆU SẢN PHẨM (CHỈ CẦN CHỈNH SỬA Ở ĐÂY)
        // =========================================================
        const productsData = [
            {
                id: 1,
                name: "男士純棉圓領短袖T恤", // Tên sản phẩm
                price: "NT$ 350",           // Giá
                image: "[https://images.unsplash.com/photo-1521572163474-6864f9cf17ab?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60](https://www.canva.com/vi_vn/do-hoa/s/hinh-anh-hoat-hinh-cute/?continuation=650)", // Link ảnh
                desc: "100%純棉材質，透氣舒適，四面彈力不緊繃。適合休閒、通勤等多種場合穿著。" // Mô tả
            },
            {
                id: 2,
                name: "無線藍牙5.0降噪耳機",
                price: "NT$ 890",
                image: "https://images.unsplash.com/photo-1590658268037-6bf12165a8df?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60",
                desc: "高音質立體聲，支援主動降噪。單次續航6小時，搭配充電盒可達24小時，輕巧好攜帶。"
            },
            {
                id: 3,
                name: "運動防水真皮錶帶手錶",
                price: "NT$ 1,250",
                image: "https://images.unsplash.com/photo-1524592094714-0f0654e20314?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60",
                desc: "商務休閒兩用，防刮藍寶石玻璃鏡面，30米生活防水，展現男士優雅品味。"
            }
            // ĐỂ THÊM SẢN PHẨM MỚI: Copy một khối { ... } ở trên, dán xuống dưới (nhớ thêm dấu phẩy) và sửa nội dung.
        ];

        // =========================================================
        // MÃ XỬ LÝ GIAO DIỆN (KHÔNG CẦN CHỈNH SỬA)
        // =========================================================
        
        // Tự động tạo thẻ sản phẩm
        const grid = document.getElementById('productGrid');
        
        productsData.forEach(product => {
            const card = document.createElement('div');
            card.className = 'product-card';
            card.onclick = () => openModal(product.id);
            
            card.innerHTML = `
                <img src="${product.image}" alt="${product.name}" class="product-img">
                <div class="product-info">
                    <div class="product-title">${product.name}</div>
                    <div class="product-price">${product.price}</div>
                </div>
            `;
            grid.appendChild(card);
        });

        // Hàm mở Modal chi tiết
        function openModal(productId) {
            const product = productsData.find(p => p.id === productId);
            if (!product) return;

            document.getElementById('modal-title').innerText = product.name;
            document.getElementById('modal-price').innerText = product.price;
            document.getElementById('modal-desc').innerText = product.desc;
            document.getElementById('modal-img').src = product.image;

            document.getElementById('productModal').style.display = "block";
        }

        // Hàm đóng Modal
        function closeModal() {
            document.getElementById('productModal').style.display = "none";
        }

        // Đóng khi click ra ngoài
        window.onclick = function(event) {
            const modal = document.getElementById('productModal');
            if (event.target == modal) {
                modal.style.display = "none";
            }
        }
    </script>
</body>
</html>
