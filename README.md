- 👋 Hi, I’m @Dean1332
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...

<!---
Dean1332/Dean1332 is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
import time
import schedule

# 假設玩家輸入的資料，包含地圖、結束時間、重生球資訊
game_data = {
    "地圖": "黑暗森林",
    "結束時間": "2025-01-07 16:00",  # 預定的結束時間
    "綠球重生時間": "每 5 分鐘",
    "藍球重生時間": "每 10 分鐘",
    "紫球重生時間": "每 15 分鐘",
    "金球重生時間": "每 20 分鐘"
}

# 顯示地圖及結束時間
def show_game_info():
    print(f"玩家目前地圖: {game_data['地圖']}")
    print(f"預定結束時間: {game_data['結束時間']}")

# 記錄重生球的資訊
def record_rebirth_times():
    print(f"綠球重生時間: {game_data['綠球重生時間']}")
    print(f"藍球重生時間: {game_data['藍球重生時間']}")
    print(f"紫球重生時間: {game_data['紫球重生時間']}")
    print(f"金球重生時間: {game_data['金球重生時間']}")

# 推算下一次重生球重生時間，若球未按時出現
def calculate_rebirth_respawn():
    print("重生球未按時出現，正在推算下一次重生時間...")
    current_time = time.localtime()  # 取得當前時間
    print(f"當前時間: {time.strftime('%Y-%m-%d %H:%M:%S', current_time)}")
    next_respawn_time = time.strftime('%Y-%m-%d %H:%M:%S', time.localtime(time.time() + 3600))  # 假設重生時間推算1小時
    print(f"下一次重生球重生時間預計為: {next_respawn_time}")
    
    # 每 10 分鐘檢查是否有球重生
    schedule.every(10).minutes.do(calculate_rebirth_respawn)

# 設定定時任務
schedule.every().day.at("12:00").do(show_game_info)
schedule.every().day.at("12:05").do(record_rebirth_times)
schedule.every().day.at("12:10").do(calculate_rebirth_respawn)

# 讓程式持續運行並執行已設定的任務
while True:
    schedule.run_pending()
    time.sleep(1)
