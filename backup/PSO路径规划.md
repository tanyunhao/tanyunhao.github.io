现有一大型零售企业的物流中心(12,12)要给10个超市送货,每个超市的需求量如下表1所示, 物流中心共5辆车,每辆车载重q为40,要给这些超市送货,车辆的单位运输成本为 c=10 元/公里,求配送费 用最低的配送方案。表1超市需求量及坐标

| 超市编号 | 需求量 | X   | Y   |
| :--- | :-- | :-- | :-- |
| 1    | 10  | 3   | 13  |
| 2    | 15  | 12  | 7   |
| 3    | 21  | 2   | 26  |
| 4    | 9   | 24  | 12  |
| 5    | 25  | 31  | 22  |
| 6    | 18  | 5   | 14  |
| 7    | 23  | 17  | 11  |
| 8    | 15  | 16  | 13  |
| 9    | 8   | 12  | 8   |
| 10   | 13  | 8   | 2   |

## 粒子群算法

1. 使用部分匹配交叉操作,确保后代没有重复元素。

2. 在适应度函数中添加了惩罚项,对重复的路线和未覆盖所有位置的解进行了惩罚。

3. 使用了锦标赛选择策略

4. 输出最优解的总距离、总花费，以及每辆车的行驶路线

5. 应该有五条路线，输出五条路线（用序号表示顺序）及每条路线的距离、花费

6. 每辆车应从物流中心出发，最后回到物流中心，这些距离和花费也要加入计算


```python
import math
import random
import numpy as np

# 超市需求量及坐标
demand = [10, 15, 21, 9, 25, 18, 23, 15, 8, 13]
x_coords = [3, 12, 2, 24, 31, 5, 17, 16, 12, 8]
y_coords = [13, 7, 26, 12, 22, 14, 11, 13, 8, 2]
num_stores = len(demand)

# 物流中心坐标
depot_x, depot_y = 12, 12

# 车辆载重量和单位运输成本
vehicle_capacity = 40
unit_cost = 10

# 蚂蚁数量和最大迭代次数
num_ants = 50
max_iterations = 100

# 信息素衰减率和启发式因子
rho = 0.5
alpha = 1.0
beta = 2.0

# 计算两点之间的欧几里得距离
def calculate_distance(x1, y1, x2, y2):
    return math.sqrt((x1 - x2) ** 2 + (y1 - y2) ** 2)

# 初始化信息素矩阵
pheromone_matrix = np.ones((num_stores + 1, num_stores + 1))

# ACO算法主函数
def aco_algorithm():
    global pheromone_matrix
    best_solution = None
    best_cost = float('inf')
    
    for iteration in range(max_iterations):
        # 构建蚂蚁集合
        ants = build_ants()
        
        # 计算每只蚂蚁的解和成本
        solutions = []
        costs = []
        for ant in ants:
            solution, cost = calculate_solution(ant)
            solutions.append(solution)
            costs.append(cost)
        
        # 更新最优解和信息素矩阵
        best_idx = np.argmin(costs)
        if costs[best_idx] < best_cost:
            best_solution = solutions[best_idx]
            best_cost = costs[best_idx]
        update_pheromone_matrix(solutions, costs)
        
        # 输出当前迭代的最优解
        #print(f"Iteration {iteration + 1}: Best cost = {best_cost}")
    
    # 输出最终最优解
    print("\nBest solution:")
    print_solution(best_solution, best_cost)

# 构建蚂蚁集合
def build_ants():
    ants = []
    for _ in range(num_ants):
        ant = [0]  # 所有蚂蚁从物流中心出发
        remaining_stores = list(range(1, num_stores + 1))
        random.shuffle(remaining_stores)
        ant.extend(remaining_stores)
        ants.append(ant)
    return ants

# 计算一只蚂蚁的解和成本
def calculate_solution(ant):
    solution = []
    current_load = 0
    current_route = [0]  # 从物流中心出发
    total_distance = 0
    
    for store in ant[1:]:
        if current_load + demand[store - 1] <= vehicle_capacity:
            current_route.append(store)
            current_load += demand[store - 1]
        else:
            total_distance += calculate_route_distance(current_route, x_coords, y_coords, depot_x, depot_y)
            solution.append(current_route)
            current_route = [0, store]
            current_load = demand[store - 1]
    
    if current_route:
        total_distance += calculate_route_distance(current_route, x_coords, y_coords, depot_x, depot_y)
        solution.append(current_route)
    
    cost = total_distance * unit_cost
    return solution, cost

# 计算一条路线的距离
def calculate_route_distance(route, x_coords, y_coords, depot_x, depot_y):
    distance = 0
    prev_x, prev_y = depot_x, depot_y
    for store in route[1:]:
        x, y = x_coords[store - 1], y_coords[store - 1]
        distance += calculate_distance(prev_x, prev_y, x, y)
        prev_x, prev_y = x, y
    distance += calculate_distance(prev_x, prev_y, depot_x, depot_y)
    return distance

# 更新信息素矩阵
def update_pheromone_matrix(solutions, costs):
    global pheromone_matrix
    pheromone_matrix *= (1 - rho)  # 信息素衰减
    
    for solution, cost in zip(solutions, costs):
        for route in solution:
            for i in range(len(route) - 1):
                pheromone_matrix[route[i], route[i + 1]] += 1.0 / cost
                pheromone_matrix[route[i + 1], route[i]] += 1.0 / cost

print("ACO算法：")

# 输出解
def print_solution(solution, cost):
    for i, route in enumerate(solution):
        route_distance = calculate_route_distance(route, x_coords, y_coords, depot_x, depot_y)
        route_cost = route_distance * unit_cost
        print(f"Vehicle {i + 1} route: 0 -> {' -> '.join(str(store) for store in route[1:])} -> 0, Distance: {route_distance}, Cost: {route_cost}")
    print(f"\nTotal cost: {cost}")

# 运行算法
aco_algorithm()
```

输出结果：
```powershell
ACO算法：

Best solution:
Vehicle 1 route: 0 -> 3 -> 1 -> 0, Distance: 39.29844048262797, Cost: 392.9844048262797
Vehicle 2 route: 0 -> 6 -> 0, Distance: 14.560219778561036, Cost: 145.60219778561037
Vehicle 3 route: 0 -> 7 -> 8 -> 0, Distance: 11.458193116710234, Cost: 114.58193116710234
Vehicle 4 route: 0 -> 9 -> 2 -> 10 -> 0, Distance: 22.173453851701858, Cost: 221.73453851701856
Vehicle 5 route: 0 -> 4 -> 5 -> 0, Distance: 45.67746616931759, Cost: 456.7746616931759

Total cost: 1331.677733989187
```

## 贪心算法

```python
import math

# 超市需求量及坐标
demand = [10, 15, 21, 9, 25, 18, 23, 15, 8, 13]
x_coords = [3, 12, 2, 24, 31, 5, 17, 16, 12, 8]
y_coords = [13, 7, 26, 12, 22, 14, 11, 13, 8, 2]
num_stores = len(demand)

# 物流中心坐标
depot_x, depot_y = 12, 12

# 车辆载重量和单位运输成本
vehicle_capacity = 40
unit_cost = 10

# 计算两点之间的欧几里得距离
def calculate_distance(x1, y1, x2, y2):
    return math.sqrt((x1 - x2) ** 2 + (y1 - y2) ** 2)

# 贪心算法求解
def greedy_solution():
    # 按需求量从大到小排序
    sorted_indices = sorted(range(num_stores), key=lambda i: demand[i], reverse=True)
    
    routes = []
    current_route = []
    current_load = 0
    
    for i in sorted_indices:
        if current_load + demand[i] <= vehicle_capacity:
            current_route.append(i + 1)
            current_load += demand[i]
        else:
            routes.append(current_route)
            current_route = [i + 1]
            current_load = demand[i]
    
    if current_route:
        routes.append(current_route)
    
    # 计算总距离和总花费
    total_distance = 0
    total_cost = 0
    
    print("贪心策略：")
    for route in routes:
        route_distance = 0
        prev_x, prev_y = depot_x, depot_y
        for store in route:
            x, y = x_coords[store - 1], y_coords[store - 1]
            route_distance += calculate_distance(prev_x, prev_y, x, y)
            prev_x, prev_y = x, y
        route_distance += calculate_distance(prev_x, prev_y, depot_x, depot_y)
        total_distance += route_distance
        total_cost += route_distance * unit_cost
        print(f"Vehicle route: 0 -> {' -> '.join(str(store) for store in route)} -> 0, Distance: {route_distance}, Cost: {route_distance * unit_cost}")
    
    print(f"\nTotal distance: {total_distance}")
    print(f"Total cost: {total_cost}")

# 运行算法
greedy_solution()
```

输出结果：

```powershell
贪心策略：
Vehicle route: 0 -> 5 -> 0, Distance: 42.941821107167776, Cost: 429.4182110716778
Vehicle route: 0 -> 7 -> 0, Distance: 10.198039027185569, Cost: 101.9803902718557
Vehicle route: 0 -> 3 -> 6 -> 0, Distance: 36.854077300218755, Cost: 368.54077300218756
Vehicle route: 0 -> 2 -> 8 -> 0, Distance: 16.33420817654564, Cost: 163.3420817654564
Vehicle route: 0 -> 10 -> 1 -> 4 -> 9 -> 0, Distance: 60.526282270165744, Cost: 605.2628227016575

Total distance: 166.8544278812835
Total cost: 1668.5442788128348
```

