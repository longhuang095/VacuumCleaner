import random

class VacuumCleaner:
    def __init__(self, room_size):
        self.room_size = room_size  # 房間的大小（假設是方形房間）
        self.position = [0, 0]  # 吸塵器的當前位置 (x, y)
        self.cleaned_area = set()  # 已清潔的區域
        self.is_cleaning = False

    def start_cleaning(self):
        self.is_cleaning = True
        print("Vacuum cleaner started cleaning.")

    def stop_cleaning(self):
        self.is_cleaning = False
        print("Vacuum cleaner stopped cleaning.")

    def move(self):
        if self.is_cleaning:
            # 隨機移動吸塵器，每次移動一個單位
            new_x = self.position[0] + random.choice([-1, 1])
            new_y = self.position[1] + random.choice([-1, 1])

            # 確保吸塵器不會移出房間邊界
            new_x = max(0, min(self.room_size - 1, new_x))
            new_y = max(0, min(self.room_size - 1, new_y))

            self.position = [new_x, new_y]
            print(f"Vacuum cleaner moved to position {self.position}.")

            # 清潔當前位置
            self.cleaned_area.add(tuple(self.position))
            print(f"Position {self.position} cleaned.")

    def detect_obstacle(self):
        # 模擬檢測障礙物的過程，假設10%的概率檢測到障礙物
        if random.random() < 0.1:
            print("Obstacle detected! Changing direction.")
            return True
        return False

    def status(self):
        cleaned_percentage = (len(self.cleaned_area) / (self.room_size ** 2)) * 100
        print(f"Cleaned {cleaned_percentage:.2f}% of the room.")

# 創建一個5x5大小的房間和吸塵器
vacuum = VacuumCleaner(5)

# 啟動清掃模式
vacuum.start_cleaning()

# 吸塵器運行模擬
for _ in range(20):  # 模擬20個移動步驟
    if vacuum.detect_obstacle():
        continue  # 如果遇到障礙物，跳過該步驟
    vacuum.move()
    vacuum.status()

# 停止清掃
vacuum.stop_cleaning()
# VacuumCleaner
