---
title: "BFS-knight"
date: 2020-06-14T23:31:11+08:00
draft: false
tags: [ "算法", "BFS"]
keywords: [ "算法", "BFS"]
---
```python
# 使用队列来做
# 从起点（sx,sy）存入队列，
# 从队列首位开始取出，然后执行进行方向移动。判断移动后的位置是否在棋盘内。是则存入队列，否则进入下一步
# 反复操作直到最后（x,y）=(ex,ey)


class Point(object):

    def __init__(self, x, y, step=0, path=[]):
        """
        knight的坐标系统
        :x: 点 x
        :y: 点 y
        :step: 记步
        :returns: 点对象
        """
        self.x = int(x)
        self.y = int(y)
        self.step = int(step)
        self.path = path

    def __repr__(self):
        return self.__str__()

    def __unicode__(self):
        return self.__str__()

    def __str__(self):
        return u"终点为<{0.x}, {0.y}>时，最短步数={0.step}".format(self)


def knight_move(size, s_point, e_point):
    """
    BFS knight movement
    :param size: 棋盘大小
    :param s_point: 起始点
    :param e_point: 终点
    :returns: 终点以及最短步数
    """
    size = int(size)
    board = [[0 for tmp_y in range(size)] for tmp_x in range(size)]
    queue = [s_point]  # 搜寻队列
    rules = ((1, 2), (2, 1),  # 1
             (1, -2), (2, -1),  # 4
             (-1, -2), (-2, -1),  # 3
             (-2, 1), (-1, 2))  # 2

    while queue:
        s_point = queue.pop(0)  # 取点
        if s_point.x == e_point.x and s_point.y == e_point.y:
            return s_point

        for direction in rules:

            next_point = Point(s_point.x + direction[0],
                               s_point.y + direction[1],
                               s_point.step + 1, )

            if (0 <= next_point.x < size and 0 <= next_point.y < size
                    and not board[next_point.y][next_point.x]):
                # 检查新的点是否有效且在图上
                next_point.path = s_point.path + [next_point]
                queue.append(next_point)
                board[next_point.y][next_point.x] = 1


result = knight_move(300, Point(0, 0), Point(11, 11))

print(result)

```