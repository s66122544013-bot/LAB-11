import heapq


# =========================
# Node Class
# =========================
class Node:
    def __init__(self, state, parent=None, action=None, path_cost=0):
        self.state = state
        self.parent = parent
        self.action = action
        self.path_cost = path_cost

    def __lt__(self, other):
        return self.path_cost < other.path_cost


# =========================
# Graph Definition (Romania Map)
# =========================
romania_graph = {
    "Arad": {"Zerind": 75, "Timisoara": 118, "Sibiu": 140},
    "Zerind": {"Arad": 75, "Oradea": 71},
    "Oradea": {"Zerind": 71, "Sibiu": 151},
    "Timisoara": {"Arad": 118, "Lugoj": 111},
    "Lugoj": {"Timisoara": 111, "Mehadia": 70},
    "Mehadia": {"Lugoj": 70, "Drobeta": 75},
    "Drobeta": {"Mehadia": 75, "Craiova": 120},
    "Craiova": {"Drobeta": 120, "Rimnicu Vilcea": 146, "Pitesti": 138},
    "Sibiu": {"Arad": 140, "Oradea": 151, "Fagaras": 99, "Rimnicu Vilcea": 80},
    "Rimnicu Vilcea": {"Sibiu": 80, "Craiova": 146, "Pitesti": 97},
    "Fagaras": {"Sibiu": 99, "Bucharest": 211},
    "Pitesti": {"Rimnicu Vilcea": 97, "Craiova": 138, "Bucharest": 101},
    "Bucharest": {"Fagaras": 211, "Pitesti": 101, "Giurgiu": 90, "Urziceni": 85},
    "Giurgiu": {"Bucharest": 90},
    "Urziceni": {"Bucharest": 85, "Hirsova": 98, "Vaslui": 142},
    "Hirsova": {"Urziceni": 98, "Eforie": 86},
    "Eforie": {"Hirsova": 86},
    "Vaslui": {"Urziceni": 142, "Iasi": 92},
    "Iasi": {"Vaslui": 92, "Neamt": 87},
    "Neamt": {"Iasi": 87},
}


# =========================
# Expand Function
# =========================
def expand(node):
    for neighbor, cost in romania_graph[node.state].items():
        yield Node(
            state=neighbor,
            parent=node,
            action=neighbor,
            path_cost=node.path_cost + cost
        )


# =========================
# Uniform Cost Search
# =========================
def uniform_cost_search(start, goal):
    node = Node(start)

    frontier = []
    heapq.heappush(frontier, (node.path_cost, node))

    reached = {start: node}

    while frontier:
        _, node = heapq.heappop(frontier)

        if node.state == goal:
            return node

        for child in expand(node):
            s = child.state

            if s not in reached or child.path_cost < reached[s].path_cost:
                reached[s] = child
                heapq.heappush(frontier, (child.path_cost, child))

    return None


# =========================
# Solution Path
# =========================
def get_path(node):
    path = []
    while node:
        path.append(node.state)
        node = node.parent
    return list(reversed(path))


# =========================
# Run Search
# =========================
if __name__ == "__main__":
    start = "Arad"
    goal = "Bucharest"

    result = uniform_cost_search(start, goal)

    if result:
        print("Path:", " -> ".join(get_path(result)))
        print("Total Cost:", result.path_cost)
    else:
        print("No solution found.")
