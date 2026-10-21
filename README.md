<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>minhFlower - Hoa tươi, yêu thương</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdn.jsdelivr.net/npm/font-awesome@4.7.0/css/font-awesome.min.css" rel="stylesheet">
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        primary: '#4F95FF',
                        secondary: '#FF6B9D',
                        accent: '#FFB74D',
                        light: '#F0F7FF',
                        pinkLight: '#FFF0F7',
                        softBlue: '#E6F0FF',
                        dark: '#2D3748'
                    },
                    fontFamily: {
                        sans: ['Poppins', 'system-ui', 'sans-serif'],
                    }
                }
            }
        }
    </script>
    <style type="text/tailwindcss">
        @layer utilities {
            .card-hover { transition: all 0.3s ease; }
            .card-hover:hover { transform: translateY(-6px); box-shadow: 0 12px 28px rgba(79, 149, 255, 0.18); }
            .bg-gradient-brand { background: linear-gradient(135deg, #4F95FF 0%, #FF6B9D 55%, #FFB74D 100%); }
            .bg-gradient-pink { background: linear-gradient(135deg, #FF6B9D 0%, #FF8FB3 100%); }
            .bg-gradient-blue { background: linear-gradient(135deg, #4F95FF 0%, #7BB3FF 100%); }
            .text-shadow-soft { text-shadow: 0 2px 4px rgba(0,0,0,0.08); }
        }
    </style>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    <style>
        * { font-family: 'Poppins', sans-serif; }
        html { scroll-behavior: smooth; }
        .hidden-section { display: none !important; }
        .nav-link { transition: all 0.25s ease; }
        .nav-link:hover { transform: translateY(-2px); }
        input, select, textarea { font-size: 1rem; }
    </style>
</head>
<body class="bg-light text-dark leading-relaxed">
    <!-- ===== THANH ĐIỀU HƯỚNG ===== -->
    <nav class="fixed w-full bg-white/95 backdrop-blur-md z-50 shadow-sm">
        <div class="container mx-auto px-4 md:px-6 py-3 flex justify-between items-center">
            <!-- Logo -->
            <a href="#trangchu" class="flex items-center gap-2 group">
                <div class="w-10 h-10 rounded-full bg-gradient-brand flex items-center justify-center text-white text-xl shadow-md group-hover:shadow-lg transition-shadow">
                    🌸
                </div>
                <span class="text-xl font-bold bg-gradient-brand bg-clip-text text-transparent">minhFlower</span>
            </a>

            <!-- Menu trên máy tính -->
            <div class="hidden md:flex items-center gap-8 lg:gap-10">
                <a href="#trangchu" class="nav-link font-medium text-gray-700 hover:text-primary px-1 py-2">Trang chủ</a>
                <a href="#sanpham" class="nav-link font-medium text-gray-700 hover:text-secondary px-1 py-2">Sản phẩm</a>
                <a href="#dichvu" class="nav-link font-medium text-gray-700 hover:text-primary px-1 py-2">Dịch vụ</a>
                <a href="#lienhe" class="nav-link font-medium text-gray-700 hover:text-secondary px-1 py-2">Liên hệ</a>
                <a href="#giohang" class="nav-link font-medium text-gray-700 hover:text-primary px-1 py-2 relative">
                    <i class="fa fa-shopping-cart mr-1"></i> Giỏ hàng
                    <span id="cartCount" class="absolute -top-1 -right-3 bg-secondary text-white text-xs w-5 h-5 rounded-full flex items-center justify-center font-bold">0</span>
                </a>
                <button id="authBtn" class="bg-gradient-brand text-white px-5 py-2.5 rounded-full font-medium hover:opacity-90 transition-opacity shadow-sm">
                    <span id="authText">Đăng nhập</span>
                </button>
            </div>

            <!-- Nút menu di động -->
            <button id="mobileMenuBtn" class="md:hidden text-dark text-2xl">
                <i class="fa fa-bars"></i>
            </button>
        </div>

        <!-- Menu trên điện thoại -->
        <div id="mobileMenu" class="md:hidden hidden bg-white border-t px-4 py-4 space-y-3">
            <a href="#trangchu" class="block py-2.5 font-medium text-gray-700 hover:text-primary">Trang chủ</a>
            <a href="#sanpham" class="block py-2.5 font-medium text-gray-700 hover:text-secondary">Sản phẩm</a>
            <a href="#dichvu" class="block py-2.5 font-medium text-gray-700 hover:text-primary">Dịch vụ</a>
            <a href="#lienhe" class="block py-2.5 font-medium text-gray-700 hover:text-secondary">Liên hệ</a>
            <a href="#giohang" class="block py-2.5 font-medium text-gray-700 hover:text-primary">
                Giỏ hàng <span id="cartCountMobile" class="bg-secondary text-white text-xs px-2 py-0.5 rounded-full ml-1">0</span>
            </a>
            <button id="mobileAuthBtn" class="w-full bg-gradient-brand text-white py-2.5 rounded-full font-medium mt-2">Đăng nhập</button>
        </div>
    </nav>

    <!-- ===== ĐĂNG NHẬP QUẢN TRỊ ===== -->
    <div id="loginModal" class="fixed inset-0 bg-black/50 z-[100] flex items-center justify-center hidden">
        <div class="bg-white rounded-3xl p-8 w-full max-w-md mx-4 shadow-2xl">
            <div class="text-center mb-6">
                <div class="w-16 h-16 rounded-full bg-gradient-brand flex items-center justify-center text-white text-2xl mx-auto mb-3">🌸</div>
                <h2 class="text-2xl font-bold text-dark">Đăng nhập quản trị</h2>
                <p class="text-gray-500 mt-2">minhFlower - Quản lý cửa hàng hoa</p>
            </div>
            
            <form id="loginForm" class="space-y-4">
                <div>
                    <label class="block mb-2 font-medium text-gray-700">Tên đăng nhập</label>
                    <input type="text" id="username" placeholder="admin" required
                           class="w-full px-4 py-3 rounded-xl border border-gray-200 focus:outline-none focus:ring-2 focus:ring-primary/50">
                </div>
                <div>
                    <label class="block mb-2 font-medium text-gray-700">Mật khẩu</label>
                    <input type="password" id="password" placeholder="••••••••••" required
                           class="w-full px-4 py-3 rounded-xl border border-gray-200 focus:outline-none focus:ring-2 focus:ring-secondary/50">
                </div>
                <p id="loginError" class="text-red-500 text-sm hidden">Tên đăng nhập hoặc mật khẩu không đúng!</p>
                <button type="submit" class="w-full bg-gradient-brand text-white py-3 rounded-xl font-medium hover:opacity-90 transition-opacity">
                    Đăng nhập <i class="fa fa-sign-in ml-1"></i>
                </button>
                <button type="button" id="closeLogin" class="w-full border border-gray-300 py-2.5 rounded-xl text-gray-600 hover:bg-gray-50 mt-2">
                    Đóng
                </button>
            </form>
        </div>
    </div>

    <!-- ===== TRANG QUẢN TRỊ ===== -->
    <section id="adminSection" class="pt-28 pb-16 hidden-section">
        <div class="container mx-auto px-4">
            <div class="mb-8 flex flex-col sm:flex-row justify-between items-start sm:items-center gap-4">
                <div>
                    <h1 class="text-3xl font-bold text-dark">Bảng điều khiển quản trị</h1>
                    <p class="text-gray-500 mt-1">Chào mừng Admin — Quản lý sản phẩm minhFlower</p>
                </div>
                <button id="logoutBtn" class="bg-red-500 text-white px-5 py-2.5 rounded-full hover:bg-red-600 transition-colors font-medium">
                    <i class="fa fa-sign-out mr-1"></i> Đăng xuất
                </button>
            </div>

            <!-- Form Thêm Sản Phẩm -->
            <div class="bg-white rounded-3xl shadow-lg p-6 md:p-8 mb-10">
                <h2 class="text-xl font-bold mb-6 flex items-center gap-3">
                    <span class="w-9 h-9 bg-gradient-brand rounded-full flex items-center justify-center text-white text-lg">+</span>
                    Thêm sản phẩm mới
                </h2>
                <form id="productForm" class="space-y-4">
                    <div class="grid md:grid-cols-2 gap-4">
                        <div>
                            <label class="block mb-2 font-medium">Tên sản phẩm *</label>
                            <input type="text" id="productName" placeholder="VD: Bó hoa hồng ngọt ngào" required
                                   class="w-full px-4 py-3 rounded-xl border border-gray-200 focus:outline-none focus:ring-2 focus:ring-primary/50">
                        </div>
                        <div>
                            <label class="block mb-2 font-medium">Giá bán (đồng) *</label>
                            <input type="number" id="productPrice" placeholder="VD: 350000" required
                                   class="w-full px-4 py-3 rounded-xl border border-gray-200 focus:outline-none focus:ring-2 focus:ring-secondary/50">
                        </div>
                    </div>
                    <div>
                        <label class="block mb-2 font-medium">Mô tả sản phẩm</label>
                        <textarea id="productDesc" rows="3" placeholder="Mô tả chi tiết bó hoa..."
                                  class="w-full px-4 py-3 rounded-xl border border-gray-200 focus:outline-none focus:ring-2 focus:ring-primary/50"></textarea>
                    </div>
                    <div>
                        <label class="block mb-2 font-medium">Đường link ảnh sản phẩm</label>
                        <input type="url" id="productImage" placeholder="https://... (để trống dùng ảnh mặc định)"
                               class="w-full px-4 py-3 rounded-xl border border-gray-200 focus:outline-none focus:ring-2 focus:ring-secondary/50">
                    </div>
                    <button type="submit"
                            class="bg-gradient-brand text-white px-8 py-3 rounded-xl font-medium hover:opacity-90 transition-opacity">
                        <i class="fa fa-plus-circle mr-2"></i> Thêm sản phẩm vào trang
                    </button>
                </form>
            </div>

            <!-- Danh sách sản phẩm đã thêm -->
            <div class="bg-white rounded-3xl shadow-lg p-6 md:p-8">
                <h2 class="text-xl font-bold mb-6">Danh sách sản phẩm đã thêm</h2>
                <div id="productList" class="space-y-4">
                    <p class="text-gray-500 italic">Sản phẩm bạn thêm sẽ hiển thị ở đây...</p>
                </div>
                <div class="mt-6">
                    <a href="#sanpham" class="inline-block bg-primary text-white px-6 py-2.5 rounded-xl hover:bg-primary/90 font-medium">
                        <i class="fa fa-eye mr-1"></i> Xem tất cả sản phẩm
                    </a>
                </div>
            </div>
        </div>
    </section>

    <!-- ===== TRANG CHÍNH ===== -->
    <div id="mainContent">
        <!-- Phần đầu trang -->
        <section id="trangchu" class="pt-28 pb-16 md:pt-36 md:pb-24">
            <div class="container mx-auto px-4">
                <div class="grid md:grid-cols-2 gap-10 items-center">
                    <div class="space-y-6">
                        <h1 class="text-[clamp(2.2rem,5vw,3.5rem)] font-bold leading-tight text-shadow-soft">
                            Những bông hoa <br>
                            <span class="bg-gradient-brand bg-clip-text text-transparent">Nét yêu thương</span> <br>
                            Gửi trọn cho người bạn yêu
                        </h1>
                        <p class="text-lg text-gray-600 max-w-lg">
                            minhFlower mang đến những bó hoa tươi mới nhất, được chọn lọc tỉ mỉ, thiết kế độc đáo cho mọi dịp đặc biệt của bạn.
                        </p>
                        <div class="flex flex-wrap gap-4">
                            <a href="#sanpham" class="bg-gradient-brand text-white px-8 py-3.5 rounded-full font-medium shadow-lg hover:shadow-xl transition-all">
                                Mua ngay <i class="fa fa-arrow-right ml-2"></i>
                            </a>
                            <a href="#lienhe" class="border-2 border-secondary text-secondary px-8 py-3.5 rounded-full font-medium hover:bg-secondary/5 transition-all">
                                Liên hệ
                            </a>
                        </div>
                    </div>
                    <div class="relative">
                        <img src="https://images.unsplash.com/photo-1490750967868-88aa4486c96d?w=600&h=700&fit=crop" 
                             alt="Bó hoa đẹp" 
                             class="rounded-3xl shadow-2xl w-full object-cover h-[480px]">
                        <div class="absolute -bottom-6 -left-6 bg-white p-5 rounded-2xl shadow-lg">
                            <p class="font-bold text-primary text-2xl">100%</p>
                            <p class="text-sm text-gray-600">Hoa tươi mỗi ngày</p>
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <!-- Sản phẩm nổi bật -->
        <section id="sanpham" class="py-20 bg-white">
            <div class="container mx-auto px-4">
                <div class="text-center mb-14">
                    <h2 class="text-[clamp(1.5rem,3vw,2.5rem)] font-bold mb-3">Sản phẩm nổi bật</h2>
                    <p class="text-gray-600 max-w-2xl mx-auto">Những bó hoa được yêu thích nhất tại minhFlower</p>
                </div>

                <div id="productGrid" class="grid sm:grid-cols-2 lg:grid-cols-3 gap-8">
                    <!-- Sản phẩm mặc định 1 -->
                    <div class="bg-pinkLight rounded-3xl overflow-hidden card-hover" data-id="default-1" data-name="Bó hoa hồng hồng ngọt ngào" data-price="350000">
                        <img src="https://images.unsplash.com/photo-1518882605630-8decd18dc924?w=400&h=400&fit=crop" 
                             alt="Hoa hồng hồng" class="w-full h-72 object-cover">
                        <div class="p-6">
                            <h3 class="font-bold text-xl mb-2">Bó hoa hồng hồng ngọt ngào</h3>
                            <p class="text-gray-600 text-base mb-4">20 bông hồng Đà Lạt tươi mới, phối lá xanh tươi mát</p>
                            <p class="font-bold text-secondary text-xl mb-4">350.000 đ</p>
                            <button class="buy-btn w-full bg-gradient-pink text-white py-3 rounded-xl font-medium hover:opacity-90 transition-opacity text-lg">
                                <i class="fa fa-shopping-cart mr-2"></i> Mua ngay
                            </button>
                        </div>
                    </div>

                    <!-- Sản phẩm mặc định 2 -->
                    <div class="bg-softBlue rounded-3xl overflow-hidden card-hover" data-id="default-2" data-name="Bó hoa hướng dương rạng rỡ" data-price="280000">
                        <img src="https://images.unsplash.com/photo-1561181286-d3fee7d55364?w=400&h=400&fit=crop" 
                             alt="Hoa hướng dương" class="w-full h-72 object-cover">
                        <div class="p-6">
                            <h3 class="font-bold text-xl mb-2">Bó hoa hướng dương rạng rỡ</h3>
                            <p class="text-gray-600 text-base mb-4">15 bông hướng dương tươi sáng, mang lại niềm vui</p>
                            <p class="font-bold text-primary text-xl mb-4">280.000 đ</p>
                            <button class="buy-btn w-full bg-gradient-blue text-white py-3 rounded-xl font-medium hover:opacity-90 transition-opacity text-lg">
                                <i class="fa fa-shopping-cart mr-2"></i> Mua ngay
                            </button>
                        </div>
                    </div>

                    <!-- Sản phẩm mặc định 3 -->
                    <div class="bg-pinkLight rounded-3xl overflow-hidden card-hover" data-id="default-3" data-name="Bó hoa cẩm tú cầu thanh lịch" data-price="420000">
                        <img src="https://images.unsplash.com/photo-1469259943454-aa100abba749?w=400&h=400&fit=crop" 
                             alt="Hoa cẩm tú cầu" class="w-full h-72 object-cover">
                        <div class="p-6">
                            <h3 class="font-bold text-xl mb-2">Bó hoa cẩm tú cầu thanh lịch</h3>
                            <p class="text-gray-600 text-base mb-4">Cẩm tú cầu kết hợp hồng trắng, sang trọng và tinh tế</p>
                            <p class="font-bold text-secondary text-xl mb-4">420.000 đ</p>
                            <button class="buy-btn w-full bg-gradient-pink text-white py-3 rounded-xl font-medium hover:opacity-90 transition-opacity text-lg">
                                <i class="fa fa-shopping-cart mr-2"></i> Mua ngay
                            </button>
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <!-- ===== GIỎ HÀNG & ĐẶT HÀNG ===== -->
        <section id="giohang" class="py-20 bg-pinkLight">
            <div class="container mx-auto px-4">
                <div class="text-center mb-14">
                    <h2 class="text-[clamp(1.5rem,3vw,2.5rem)] font-bold mb-3">🛒 Giỏ hàng & Đặt hàng</h2>
                    <p class="text-gray-600 max-w-2xl mx-auto">Xem lại sản phẩm và điền thông tin giao hàng</p>
                </div>

                <div class="max-w-4xl mx-auto space-y-6">
                    <!-- Danh sách sản phẩm trong giỏ -->
                    <div class="bg-white p-6 md:p-8 rounded-3xl shadow-lg">
                        <h3 class="text-xl font-bold mb-5 text-dark">Sản phẩm đã chọn</h3>
                        <div id="cartItems">
                            <p class="text-gray-500 italic text-center py-6">Giỏ hàng đang trống — <a href="#sanpham" class="text-primary font-medium">Đi chọn hoa ngay</a></p>
                        </div>
                        <div id="orderSummary" class="mt-5 pt-5 border-t hidden">
                            <p class="text-lg font-medium">Tổng tiền: <span id="totalPrice" class="text-secondary font-bold text-xl">0 đ</span></p>
                        </div>
                    </div>

                    <!-- Thông tin đặt hàng - Luôn ở đây, không tách ra -->
                    <div class="bg-white p-6 md:p-8 rounded-3xl shadow-lg">
                        <h3 class="text-xl font-bold mb-6 text-dark">Thông tin giao hàng</h3>
                        <form id="orderForm" class="space-y-4">
                            <div class="grid md:grid-cols-2 gap-4">
                                <div>
                                    <label class="block mb-2 font-medium">Họ và tên khách hàng *</label>
                                    <input type="text" id="customerName" placeholder="Nguyễn Văn A" required
                                           class="w-full px-4 py-3 rounded-xl border border-gray-200 focus:outline-none focus:ring-2 focus:ring-primary/50">
                                </div>
                                <div>
                                    <label class="block mb-2 font-medium">Số điện thoại *</label>
                                    <input type="tel" id="customerPhone" placeholder="0397321270" required
                                           class="w-full px-4 py-3 rounded-xl border border-gray-200 focus:outline-none focus:ring-2 focus:ring-secondary/50">
                                </div>
                            </div>
                            <div>
                                <label class="block mb-2 font-medium">Địa chỉ giao hàng *</label>
                                <input type="text" id="customerAddress" placeholder="Số nhà, đường, phường, quận, thành phố" required
                                       class="w-full px-4 py-3 rounded-xl border border-gray-200 focus:outline-none focus:ring-2 focus:ring-primary/50">
                            </div>
                            <div class="grid md:grid-cols-2 gap-4">
                                <div>
                                    <label class="block mb-2 font-medium">Ngày giao mong muốn *</label>
                                    <input type="date" id="deliveryDate" required
                                           class="w-full px-4 py-3 rounded-xl border border-gray-200 focus:outline-none focus:ring-2 focus:ring-secondary/50">
                                </div>
                                <div>
                                    <label class="block mb-2 font-medium">Thời gian giao mong muốn *</label>
                                    <select id="deliveryTime" required
                                            class="w-full px-4 py-3 rounded-xl border border-gray-200 focus:outline-none focus:ring-2 focus:ring-primary/50">
                                        <option value="">-- Chọn khung giờ --</option>
                                        <option value="08:00 - 10:00">08:00 - 10:00 (Sáng sớm)</option>
                                        <option value="10:00 - 12:00">10:00 - 12:00 (Buổi sáng)</option>
                                        <option value="13:00 - 15:00">13:00 - 15:00 (Buổi trưa)</option>
                                        <option value="15:00 - 18:00">15:00 - 18:00 (Chiều tối)</option>
                                        <option value="Bất kỳ khi nào">Bất kỳ khi nào phù hợp</option>
                                    </select>
                                </div>
                            </div>
                            <div>
                                <label class="block mb-2 font-medium">Lời nhắn / Yêu cầu khác</label>
                                <textarea id="customerNote" rows="3" placeholder="Ghi chú, lời chúc kèm theo..."
                                          class="w-full px-4 py-3 rounded-xl border border-gray-200 focus:outline-none focus:ring-2 focus:ring-secondary/50"></textarea>
                            </div>
                            
                            <button type="submit" id="submitOrder"
                                    class="w-full bg-gradient-brand text-white py-3.5 rounded-xl font-medium hover:opacity-90 transition-opacity text-lg mt-2">
                                <i class="fa fa-check-circle mr-2"></i> Xác nhận đặt hàng
                            </button>
                        </form>
                    </div>
                </div>
            </div>
        </section>

        <!-- Dịch vụ -->
        <section id="dichvu" class="py-20 bg-gradient-to-b from-softBlue to-pinkLight">
            <div class="container mx-auto px-4">
                <div class="text-center mb-14">
                    <h2 class="text-[clamp(1.5rem,3vw,2.5rem)] font-bold mb-3">Tại sao chọn minhFlower?</h2>
                    <p class="text-gray-600 max-w-2xl mx-auto">Chúng tôi luôn đặt trái tim vào từng bó hoa, mang đến trải nghiệm tốt nhất cho bạn</p>
                </div>

                <div class="grid md:grid-cols-3 gap-8">
                    <div class="bg-white p-8 rounded-3xl shadow-sm text-center card-hover">
                        <div class="w-16 h-16 bg-primary/10 rounded-full flex items-center justify-center text-primary text-2xl mx-auto mb-5">
                            <i class="fa fa-leaf"></i>
                        </div>
                        <h3 class="font-bold text-xl mb-3">Hoa tươi mỗi ngày</h3>
                        <p class="text-gray-600">Nguồn hoa trực tiếp từ vườn Đà Lạt, nhập mới mỗi sáng đảm bảo độ tươi tối đa</p>
                    </div>

                    <div class="bg-white p-8 rounded-3xl shadow-sm text-center card-hover">
                        <div class="w-16 h-16 bg-secondary/10 rounded-full flex items-center justify-center text-secondary text-2xl mx-auto mb-5">
                            <i class="fa fa-truck"></i>
                        </div>
                        <h3 class="font-bold text-xl mb-3">Giao hàng nhanh</h3>
                        <p class="text-gray-600">Giao trong vòng 2 giờ tại nội thành Hà Nội, đúng giờ và đúng địa điểm yêu cầu</p>
                    </div>

                    <div class="bg-white p-8 rounded-3xl shadow-sm text-center card-hover">
                        <div class="w-16 h-16 bg-accent/10 rounded-full flex items-center justify-center text-accent text-2xl mx-auto mb-5">
                            <i class="fa fa-gift"></i>
                        </div>
                        <h3 class="font-bold text-xl mb-3">Thiết kế riêng</h3>
                        <p class="text-gray-600">Tùy chỉnh theo yêu cầu: sinh nhật, tình yêu, khai trương, lễ tân...</p>
                    </div>
                </div>
            </div>
        </section>

        <!-- Liên hệ -->
        <section id="lienhe" class="py-20 bg-white">
            <div class="container mx-auto px-4">
                <div class="grid md:grid-cols-2 gap-12 items-center">
                    <div>
                        <h2 class="text-[clamp(1.5rem,3vw,2.5rem)] font-bold mb-5">Liên hệ với chúng tôi</h2>
                        <p class="text-gray-600 mb-8">Mọi yêu cầu đặc biệt — liên hệ ngay, chúng tôi trả lời trong vòng 15 phút!</p>
                        
                        <ul class="space-y-4 mb-8">
                            <li class="flex items-center gap-3">
                                <span class="w-9 h-9 bg-primary/10 rounded-full flex items-center justify-center text-primary">
                                    <i class="fa fa-map-marker"></i>
                                </span>
                                <span>Hưng Yên - Tiên Lữ/span>
                            </li>
                            <li class="flex items-center gap-3">
                                <span class="w-9 h-9 bg-secondary/10 rounded-full flex items-center justify-center text-secondary">
                                    <i class="fa fa-phone"></i>
                                </span>
                                <span>0397321270</span>
                            </li>
                            <li class="flex items-center gap-3">
                                <span class="w-9 h-9 bg-primary/10 rounded-full flex items-center justify-center text-primary">
                                    <i class="fa fa-envelope"></i>
                                </span>
                                <span>minhminh130523@gmail.com</span>
                            </li>
                            <li class="flex items-center gap-3">
                                <span class="w-9 h-9 bg-accent/10 rounded-full flex items-center justify-center text-accent">
                                    <i class="fa fa-clock-o"></i>
                                </span>
                                <span>8:00 - 21:00 mỗi ngày</span>
                            </li>
                        </ul>
                        
                        <div class="flex gap-4 text-2xl">
                            <a href="#" class="text-primary hover:opacity-80"><i class="fa fa-facebook-square"></i></a>
                            <a href="#" class="text-secondary hover:opacity-80"><i class="fa fa-instagram"></i></a>
                            <a href="#" class="text-accent hover:opacity-80"><i class="fa fa-wechat"></i></a>
                        </div>
                    </div>

                    <div class="bg-pinkLight p-8 rounded-3xl">
                        <h3 class="text-xl font-bold mb-4">Gửi tin nhắn</h3>
                        <form class="space-y-5">
                            <div>
                                <label class="block mb-2 font-medium">Họ và tên</label>
                                <input type="text" placeholder="Nhập tên của bạn" 
                                       class="w-full px-4 py-3 rounded-xl border border-gray-200 focus:outline-none focus:ring-2 focus:ring-secondary/50">
                            </div>
                            <div>
                                <label class="block mb-2 font-medium">Số điện thoại</label>
                                <input type="tel" placeholder="0397321270" 
                                       class="w-full px-4 py-3 rounded-xl border border-gray-200 focus:outline-none focus:ring-2 focus:ring-primary/50">
                            </div>
                            <div>
                                <label class="block mb-2 font-medium">Nội dung</label>
                                <textarea rows="4" placeholder="Bạn muốn hỏi gì..." 
                                          class="w-full px-4 py-3 rounded-xl border border-gray-200 focus:outline-none focus:ring-2 focus:ring-secondary/50"></textarea>
                            </div>
                            <button type="submit" 
                                    class="w-full bg-gradient-brand text-white py-3 rounded-xl font-medium hover:opacity-90 transition-opacity">
                                Gửi tin <i class="fa fa-paper-plane ml-1"></i>
                            </button>
                        </form>
                    </div>
                </div>
            </div>
        </section>
    </div>

    <!-- Chân trang -->
    <footer class="bg-dark text-white pt-14 pb-8">
        <div class="container mx-auto px-4">
            <div class="grid md:grid-cols-4 gap-10 mb-10">
                <div class="md:col-span-2">
                    <a href="#trangchu" class="flex items-center gap-2 text-2xl font-bold mb-4 inline-block">
                        <span class="w-8 h-8 rounded-full bg-gradient-brand flex items-center justify-center text-white text-sm">🌸</span>
                        <span class="bg-gradient-brand bg-clip-text text-transparent">minhFlower</span>
                    </a>
                    <p class="text-gray-400 max-w-md mb-4">
                        Chúng tôi mang đến những bó hoa đẹp nhất, gửi gắm yêu thương đến người bạn trân quý.
                    </p>
                    <p class="text-gray-400">Mang hạnh phúc đến mọi nhà 🌷</p>
                </div>
                <div>
                    <h4 class="font-bold text-lg mb-4">Liên kết nhanh</h4>
                    <ul class="space-y-2 text-gray-400">
                        <li><a href="#trangchu" class="hover:text-primary transition-colors">Trang chủ</a></li>
                        <li><a href="#sanpham" class="hover:text-secondary transition-colors">Sản phẩm</a></li>
                        <li><a href="#giohang" class="hover:text-primary transition-colors">Đặt hàng</a></li>
                        <li><a href="#lienhe" class="hover:text-secondary transition-colors">Liên hệ</a></li>
                    </ul>
                </div>
                <div>
                    <h4 class="font-bold text-lg mb-4">Liên hệ</h4>
                    <ul class="space-y-2 text-gray-400">
                        <li>📧 minhminh130523@gmail.com</li>
                        <li>📞 0397321270</li>
                        <li>📍 Hưng Yên - Tiên Lữ</li>
                    </ul>
                </div>
            </div>
            <div class="border-t border-gray-800 pt-8 text-center text-gray-500 text-sm">
                <p>© 2026 minhFlower. Tất cả quyền được bảo lưu.</p>
            </div>
        </div>
    </footer>

    <!-- ===== JAVASCRIPT CHỨC NĂNG ===== -->
    <script>
        // Tài khoản quản trị
        const ADMIN_USER = "admin";
        const ADMIN_PASS = "Ab@12345678@";
        const YOUR_EMAIL = "minhminh1305232@gmail.com";

        let isLoggedIn = false;
        let products = [];
        let cart = [];

        // Các phần tử
        const loginModal = document.getElementById('loginModal');
        const authBtn = document.getElementById('authBtn');
        const mobileAuthBtn = document.getElementById('mobileAuthBtn');
        const authText = document.getElementById('authText');
        const loginForm = document.getElementById('loginForm');
        const closeLogin = document.getElementById('closeLogin');
        const loginError = document.getElementById('loginError');
        const adminSection = document.getElementById('adminSection');
        const mainContent = document.getElementById('mainContent');
        const logoutBtn = document.getElementById('logoutBtn');
        const productForm = document.getElementById('productForm');
        const productGrid = document.getElementById('productGrid');
        const productList = document.getElementById('productList');
        const mobileMenuBtn = document.getElementById('mobileMenuBtn');
        const mobileMenu = document.getElementById('mobileMenu');
        const cartCountEl = document.getElementById('cartCount');
        const cartCountMobileEl = document.getElementById('cartCountMobile');
        const cartItemsEl = document.getElementById('cartItems');
        const orderSummaryEl = document.getElementById('orderSummary');
        const totalPriceEl = document.getElementById('totalPrice');
        const orderForm = document.getElementById('orderForm');

        // Cập nhật số lượng giỏ hàng
        function updateCartCount() {
            const count = cart.length;
            cartCountEl.textContent = count;
            cartCountMobileEl.textContent = count;
        }

        // Hiển thị sản phẩm trong giỏ hàng
        function renderCart() {
            if (cart.length === 0) {
                cartItemsEl.innerHTML = `<p class="text-gray-500 italic text-center py-6">Giỏ hàng đang trống — <a href="#sanpham" class="text-primary font-medium">Đi chọn hoa ngay</a></p>`;
                orderSummaryEl.classList.add('hidden');
                return;
            }

            orderSummaryEl.classList.remove('hidden');
            let total = 0;
            cartItemsEl.innerHTML = '';
            
            cart.forEach((item, index) => {
                total += item.price;
                const itemEl = document.createElement('div');
                itemEl.className = 'flex justify-between items-center py-4 border-b border-gray-100 last:border-b-0';
                itemEl.innerHTML = `
                    <div>
                        <p class="font-medium text-lg">${item.name}</p>
                        <p class="text-sm text-gray-500">${item.price.toLocaleString('vi-VN')} đ</p>
                    </div>
                    <button class="text-red-500 hover:text-red-700 remove-item font-medium" data-index="${index}">
                        <i class="fa fa-trash"></i> Xóa
                    </button>
                `;
                cartItemsEl.appendChild(itemEl);
            });

            totalPriceEl.textContent = total.toLocaleString('vi-VN') + ' đ';

            // Gắn sự kiện xóa
            cartItemsEl.querySelectorAll('.remove-item').forEach(btn => {
                btn.addEventListener('click', function() {
                    const idx = parseInt(this.getAttribute('data-index'));
                    cart.splice(idx, 1);
                    updateCartCount();
                    renderCart();
                });
            });
        }

        // Bấm Mua ngay → thêm vào giỏ + nhảy xuống đặt hàng
        document.addEventListener('click', function(e) {
            if (e.target.closest('.buy-btn')) {
                const card = e.target.closest('[data-id]');
                const name = card.getAttribute('data-name');
                const price = parseInt(card.getAttribute('data-price'));
                
                cart.push({ name, price });
                updateCartCount();
                renderCart();
                
                // Hiệu ứng thông báo
                const btn = e.target.closest('.buy-btn');
                const originalText = btn.innerHTML;
                btn.innerHTML = '<i class="fa fa-check"></i> Đã thêm!';
                btn.classList.add('bg-green-500');
                
                setTimeout(() => {
                    btn.innerHTML = originalText;
                    btn.classList.remove('bg-green-500');
                }, 1500);

                // Tự động cuộn xuống phần đặt hàng
                setTimeout(() => {
                    document.getElementById('giohang').scrollIntoView({ behavior: 'smooth' });
                }, 300);
            }
        });

        // Xử lý đặt hàng + Gửi thông báo về email
        orderForm.addEventListener('submit', function(e) {
            e.preventDefault();
            
            if (cart.length === 0) {
                alert('⚠️ Giỏ hàng đang trống! Vui lòng chọn sản phẩm trước khi đặt hàng.');
                return;
            }

            const name = document.getElementById('customerName').value.trim();
            const phone = document.getElementById('customerPhone').value.trim();
            const address = document.getElementById('customerAddress').value.trim();
            const date = document.getElementById('deliveryDate').value;
            const time = document.getElementById('deliveryTime').value;
            const note = document.getElementById('customerNote').value.trim() || 'Không có';

            if (!name || !phone || !address || !date || !time) {
                alert('⚠️ Vui lòng điền đầy đủ thông tin bắt buộc!');
                return;
            }

            // Tính tổng tiền
            const total = cart.reduce((sum, item) => sum + item.price, 0);
            
            // Nội dung đơn hàng
            const orderContent = `
📋 ĐƠN HÀNG MỚI - minhFlower
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
👤 Họ tên: ${name}
📞 Số điện thoại: ${phone}
📍 Địa chỉ giao hàng: ${address}
📅 Ngày giao: ${date}
⏰ Thời gian giao: ${time}
📝 Lời nhắn: ${note}
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
🛒 Sản phẩm đã đặt:
${cart.map((item, i) => `  ${i+1}. ${item.name} — ${item.price.toLocaleString('vi-VN')} đ`).join('\n')}
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
💰 TỔNG TIỀN: ${total.toLocaleString('vi-VN')} đ
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Trân trọng, minhFlower 🌸
            `;

            // Thông báo cho khách
            alert('✅ Đặt hàng thành công!\n\n' + orderContent + '\n\n📧 Thông báo đã được gửi đến email của bạn!');

            // Mở ứng dụng gửi thư trên máy/điện thoại
            const subject = encodeURIComponent('Đơn hàng mới từ minhFlower - ' + name);
            const body = encodeURIComponent(orderContent);
            window.location.href = `mailto:${YOUR_EMAIL}?subject=${subject}&body=${body}`;

            // Reset sau khi đặt hàng
            cart = [];
            updateCartCount();
            renderCart();
            orderForm.reset();
        });

        // Mở/đóng menu di động
        mobileMenuBtn.addEventListener('click', () => {
            mobileMenu.classList.toggle('hidden');
        });

        // Mở form đăng nhập
        function openLoginModal() {
            if (isLoggedIn) {
                mainContent.classList.add('hidden-section');
                adminSection.classList.remove('hidden-section');
            } else {
                loginModal.classList.remove('hidden');
                loginError.classList.add('hidden');
                document.getElementById('username').value = '';
                document.getElementById('password').value = '';
            }
        }
        authBtn.addEventListener('click', openLoginModal);
        mobileAuthBtn.addEventListener('click', openLoginModal);

        // Đóng form đăng nhập
        closeLogin.addEventListener('click', () => {
            loginModal.classList.add('hidden');
        });

        // Đăng nhập
        loginForm.addEventListener('submit', (e) => {
            e.preventDefault();
            const user = document.getElementById('username').value.trim();
            const pass = document.getElementById('password').value;

            if (user === ADMIN_USER && pass === ADMIN_PASS) {
                isLoggedIn = true;
                loginModal.classList.add('hidden');
                authText.textContent = "Quản trị";
                mobileAuthBtn.textContent = "Quản trị";
                mainContent.classList.add('hidden-section');
                adminSection.classList.remove('hidden-section');
            } else {
                loginError.classList.remove('hidden');
            }
        });

        // Đăng xuất
        logoutBtn.addEventListener('click', () => {
            isLoggedIn = false;
            authText.textContent = "Đăng nhập";
            mobileAuthBtn.textContent = "Đăng nhập";
            adminSection.classList.add('hidden-section');
            mainContent.classList.remove('hidden-section');
            window.location.hash = '#trangchu';
        });

        // Thêm sản phẩm - ĐÃ SỬA LỖI
        productForm.addEventListener('submit', (e) => {
            e.preventDefault();
            
            const name = document.getElementById('productName').value.trim();
            const price = document.getElementById('productPrice').value;
            const desc = document.getElementById('productDesc').value.trim() || 'Sản phẩm mới từ minhFlower';
            const img = document.getElementById('productImage').value.trim() || 'https://images.unsplash.com/photo-1525310072745-f49212b5ac6d?w=400&h=400&fit=crop';

            if (!name || !price) {
                alert('⚠️ Vui lòng điền đầy đủ Tên sản phẩm và Giá bán!');
                return;
            }

            const newProduct = {
                id: Date.now(),
                name: name,
                price: parseInt(price),
                desc: desc,
                img: img
            };
            
            products.push(newProduct);
            
            // Thêm vào lưới sản phẩm ngay lập tức
            const isPink = products.length % 2 === 0;
            const cardBg = isPink ? 'bg-pinkLight' : 'bg-softBlue';
            const btnBgClass = isPink ? 'bg-gradient-pink' : 'bg-gradient-blue';
            
            const newCard = document.createElement('div');
            newCard.className = `${cardBg} rounded-3xl overflow-hidden card-hover`;
            newCard.setAttribute('data-id', newProduct.id);
            newCard.setAttribute('data-name', newProduct.name);
            newCard.setAttribute('data-price', newProduct.price);
            newCard.innerHTML = `
                <img src="${newProduct.img}" alt="${newProduct.name}" class="w-full h-72 object-cover">
                <div class="p-6">
                    <h3 class="font-bold text-xl mb-2">${newProduct.name}</h3>
                    <p class="text-gray-600 text-base mb-4">${newProduct.desc}</p>
                    <p class="font-bold ${isPink ? 'text-secondary' : 'text-primary'} text-xl mb-4">${newProduct.price.toLocaleString('vi-VN')} đ</p>
                    <button class="buy-btn w-full ${btnBgClass} text-white py-3 rounded-xl font-medium hover:opacity-90 transition-opacity text-lg">
                        <i class="fa fa-shopping-cart mr-2"></i> Mua ngay
                    </button>
                </div>
            `;
            productGrid.appendChild(newCard);
            
            // Cập nhật danh sách quản trị
            updateAdminProductList();
            
            // Reset form
            productForm.reset();
            alert('✅ Sản phẩm "' + newProduct.name + '" đã được thêm thành công!');
        });

        // Cập nhật danh sách trong quản trị
        function updateAdminProductList() {
            if (products.length === 0) {
                productList.innerHTML = '<p class="text-gray-500 italic">Sản phẩm bạn thêm sẽ hiển thị ở đây...</p>';
                return;
            }
            
            productList.innerHTML = '';
            products.forEach((p, index) => {
                const item = document.createElement('div');
                item.className = 'flex justify-between items-center p-4 bg-gray-50 rounded-xl';
                item.innerHTML = `
                    <div>
                        <p class="font-medium text-lg">${p.name}</p>
                        <p class="text-sm text-gray-500">${p.price.toLocaleString('vi-VN')} đ</p>
                    </div>
                    <button class="text-red-500 hover:text-red-700 font-medium" data-index="${index}">
                        <i class="fa fa-trash"></i> Xóa
                    </button>
                `;
                productList.appendChild(item);
            });
            
            productList.querySelectorAll('button[data-index]').forEach(btn => {
                btn.addEventListener('click', function() {
                    const idx = parseInt(this.getAttribute('data-index'));
                    if (confirm('Bạn có chắc muốn xóa sản phẩm này?')) {
                        products.splice(idx, 1);
                        window.location.reload();
                    }
                });
            });
        }

        // Liên kết mượt mà
        document.querySelectorAll('a[href^="#"]').forEach(anchor => {
            anchor.addEventListener('click', function(e) {
                const href = this.getAttribute('href');
                if (href === '#') return;
                
                const targetId = href.substring(1);
                const target = document.getElementById(targetId);
                if (target) {
                    e.preventDefault();
                    if (isLoggedIn && ['trangchu','sanpham','dichvu','lienhe','giohang'].includes(targetId)) {
                        adminSection.classList.add('hidden-section');
                        mainContent.classList.remove('hidden-section');
                    }
                    window.location.hash = href;
                    mobileMenu.classList.add('hidden');
                }
            });
        });
    </script>
</body>
</html>
