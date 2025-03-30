
Lối chơi, logic của game:
Link game youtube: https://www.youtube.com/watch?v=trh_7l8rVI4
Lối chơi
   1.Cấu trúc chính của game: 
     o	Người chơi điều khiển một nhân vật chính (MainObject)
     o	Game bắt đầu với màn hình menu
     o	Mỗi lượt chơi có thời gian giới hạn (300 giây)
     o	Người chơi có 3 mạng ban đầu (hiển thị bởi PlayerPower)
   2.Mục tiêu: 
      o	Di chuyển qua các map
      o	Tiêu diệt kẻ địch (threats)
      o	Thu thập tiền
      o	Chiến đấu và đánh bại boss ở cuối map
    3.Hệ thống điểm (Mark): 
      o	Tiêu diệt kẻ địch thông thường: +1 điểm
      o	Gây sát thương cho boss: +5 điểm
Logic game
     1.	Vòng lặp chính: 
      o	Game chạy trong một vòng lặp while cho đến khi người chơi thoát hoặc kết thúc
      o	Giới hạn FPS bằng ImpTimer
      o	Mỗi frame xử lý input, cập nhật trạng thái, và render
     2.	Hệ thống nhân vật và kẻ địch: 
      o	Nhân vật chính (MainObject): 
      o	Di chuyển trái/phải, nhảy
      o	Bắn đạn để tiêu diệt kẻ địch
      o	Có khả năng va chạm với tiles, kẻ địch, boss và items
      o	Kẻ địch (ThreatsObject): 
      o	Có hai loại chính: di chuyển tĩnh (STATIC_TH) và di chuyển trong khoảng (MOVE_IN_SPACE_TH)
      o	Có thể bắn đạn tấn công người chơi
      o	Biến mất khi bị tiêu diệt
      o	Boss: 
      o	Xuất hiện ở cuối map
      o	Có hệ thống máu riêng (health)
      o	Bắn đạn tấn công người chơi
      o	Cần nhiều phát bắn để tiêu diệt
     3.	Hệ thống items và power-ups: 
      o	Heart Items: Tăng mạng cho người chơi
      o	Money (Tiền): Thu thập 10 đồng tiền sẽ tăng thêm 1 mạng
     4.	Hệ thống mạng và chết: 
      o	Người chơi bắt đầu với 3 mạng
      o	Mất mạng khi va chạm với kẻ địch, đạn của kẻ địch, hoặc boss
      o	Khi chết, người chơi hồi sinh ở đầu map và tiếp tục chơi
      o	Game over khi mất hết mạng (num_die > 3)
     5.	Điều kiện chiến thắng/thua: 
      o	Chiến thắng: Tiêu diệt boss
      o	Thua: Hết mạng hoặc hết thời gian (300 giây)
     6.	Cơ chế tương tác với môi trường: 
      o	Map được tải từ file
      o	Va chạm với tiles (tường, nền)
      o	Scrolling theo vị trí người chơi
Đặc điểm nổi bật
     1.	Hệ thống tiền và mạng: Thu thập tiền không chỉ để tăng điểm mà còn có thể đổi lấy mạng (10 tiền = 1 mạng)
     2.	Cơ chế boss: Boss xuất hiện ở cuối map với âm thanh đặc biệt, yêu cầu nhiều phát bắn để tiêu diệt, và có thời gian chờ sau khi tiêu diệt boss trước khi hiển thị màn hình chiến thắng
     3.	Heart Items: Phân bố trên map, cho phép người chơi tăng mạng khi thu thập
     4.	Hiệu ứng nổ: Khi nhân vật hoặc kẻ địch bị tiêu diệt, có hiệu ứng nổ và âm thanh tương ứng

Đồ họa, âm thanh:
Đồ họa:
     1.	Thư viện sử dụng: Trò chơi sử dụng SDL2 (Simple DirectMedia Layer) và SDL_image để xử lý đồ họa.
     2.	Độ phân giải: Màn hình có kích thước 1280x640 pixel (SCREEN_WIDTH x SCREEN_HEIGHT).
     3.	Loại hình ảnh: Chủ yếu sử dụng file PNG cho các sprite và hình ảnh nền.
     4.	Hiệu ứng đồ họa: 
      o	Có hiệu ứng nổ khi nhân vật chết hoặc khi tiêu diệt kẻ địch
      o	Có hiệu ứng fade-in khi hiển thị màn hình chiến thắng
      o	Có các hiệu ứng animation cho nhân vật, kẻ địch và boss
     5.	Giao diện: 
      o	Có màn hình menu với nút Start
      o	Có màn hình game over với thông báo và nút
      o	Có màn hình chiến thắng với hiệu ứng fade
Âm thanh:
     1.	Thư viện sử dụng: SDL_mixer để xử lý âm thanh.
     2.	Chất lượng: Âm thanh được cấu hình ở 44100Hz, định dạng MIX_DEFAULT_FORMAT, 2 kênh.
     3 Xử lý âm thanh: 
      o	Âm thanh được bật/tắt thông qua define USE_AUDIO
      o	Nhạc nền chơi liên tục (Mix_PlayChannel(-1, g_sound_background, -1))
      o	Âm lượng được điều chỉnh khi gặp boss (giảm âm lượng nhạc nền xuống một nửa)
      o	Âm thanh dừng khi game over hoặc chiến thắng

Cấu trúc của project game:
     1.	img/: Chứa các tài nguyên hình ảnh 
      	o	background.png
	o	threat_left.png
	o	threat_level.png
	o	boss_object.png
	o	exp3.png
	o	menugame.png
	o	start_button.png
	o	button.png
      	o	victory.png
      	o	heart_item.png
     2.	font/: Chứa font chữ 
	o	dlxfont.ttf
	3.	sound/: Chứa các file âm thanh 
	o	gunshot.wav
	o	gunShot3.wav
	o	Explosion.wav
	o	player_die.wav
	o	jump.wav
	o	collectCoin.wav
	o	background.wav
	4.	map/: Chứa dữ liệu bản đồ 
	o	map01.dat
Các lớp chính
	1.	Lớp đối tượng cơ bản: 
	o	BaseObject: Lớp cơ sở cho các đối tượng game
	o	ThreatsObject: Quản lý kẻ địch thông thường
	o	BossObject: Quản lý boss
	o	MainObject: Quản lý nhân vật người chơi
	o	BulletObject: Quản lý đạn
	2.	Lớp quản lý map và hiển thị: 
	o	GameMap: Quản lý bản đồ và các tile
	o	Gemometric: Vẽ các hình học cơ bản (hình chữ nhật, đường viền)
	3	.	Lớp UI và hiệu ứng: 
	o	TextObject: Hiển thị văn bản
	o		ExplosionObject: Hiệu ứng nổ
	o	PlayerPower: Hiển thị mạng sống
	o	PlayerMoney: Hiển thị tiền
	o	HeartItem: Vật phẩm hồi máu
	4.	Lớp phụ trợ: 
	o	ImpTimer: Quản lý thời gian và FPS
	o	CommonFunc: Chứa các hàm tiện ích
Luồng xử lý chính
	1.	Khởi tạo: 
	o	Khởi tạo SDL, SDL_image, SDL_ttf, SDL_mixer
	o	Tải tài nguyên (ảnh, âm thanh, font)
	o	Hiển thị menu game
	2.	Vòng lặp game: 
	o	Xử lý input từ người chơi
	o	Cập nhật trạng thái các đối tượng
	o	Xử lý va chạm
	o	Render màn hình
	o	Kiểm soát FPS
	3.	Kết thúc: 
	o	Hiển thị màn hình chiến thắng hoặc game over
	o	Giải phóng tài nguyên
	o	Quay lại menu hoặc thoát game

Các chức năng đã cài được cho game:
	1 Hệ thống menu 
	o	Menu chính với nút Start
	o	Màn hình game over với thông báo và nút quay lại menu
	o	Màn hình chiến thắng với hiệu ứng fade-in
	2  Điều khiển nhân vật 
	o	Di chuyển trái, phải
	o	Nhảy
	o	Bắn đạn
3  Hệ thống nhân vật 
	o	Nhân vật chính với animation
	o	Các loại kẻ địch thường
	o	Boss với hệ thống máu riêng biệt
4  Bản đồ và môi trường 
	o	Tải bản đồ từ file (.dat)
	o	Vẽ các tile map
	o	Background với hiệu ứng cuộn
5  Hệ thống va chạm 
	o	Va chạm giữa nhân vật và địa hình
	o	Va chạm giữa đạn và kẻ địch
	o	Va chạm giữa đạn và boss
	o	Va chạm giữa nhân vật và kẻ địch/boss
6  UI và hiển thị 
	o	Hiển thị mạng sống người chơi
	o	Hiển thị số tiền/điểm
	o	Hiển thị thời gian còn lại
	o	Hiển thị điểm số
7  Hệ thống âm thanh 
	o	Nhạc nền liên tục
	o	Hiệu ứng âm thanh cho các hành động (bắn, nhảy, trúng đạn, nổ)
	o	Âm thanh khi nhặt item
	o	Điều chỉnh âm lượng khi gặp boss
8  Hệ thống vật phẩm 
	o	Item trái tim để hồi máu
	o	Hệ thống tiền/xu có thể đổi mạng
9  Hiệu ứng đồ họa 
o	Hiệu ứng nổ khi tiêu diệt kẻ địch
o	Hiệu ứng nổ khi nhân vật bị đánh trúng
o	Animation cho nhân vật và kẻ địch
10  Game loop và quản lý trạng thái 
o	Vòng lặp game với kiểm soát FPS
o	Cơ chế restart game từ menu
o	Quản lý thời gian và điều kiện chiến thắng/thua
11  Trí tuệ nhân tạo đơn giản 
o	Kẻ địch di chuyển theo kiểu MOVE_IN_SPACE_TH (trong một phạm vi giới hạn)
o	Kẻ địch STATIC_TH (đứng yên và bắn)
o	Boss với hành vi riêng (di chuyển và bắn)
12  Cơ chế tiến trình game 
o	Hệ thống mạng có thể hồi lại bằng item hoặc tiền
o	Giới hạn thời gian
o	Boss xuất hiện khi người chơi đến cuối map
o	Điều kiện chiến thắng khi tiêu diệt boss
Cách chơi:
Các nút điều khiển:
Di chuyển nhân vật: 
o	Phím mũi tên trái (←): Di chuyển nhân vật sang trái
o	Phím mũi tên phải (→): Di chuyển nhân vật sang phải
o	Phím mũi tên lên (↑) hoặc Phím Space: Nhảy
o	Chuột phải: Để bắn
o	Chuột trái: Để nhảy



