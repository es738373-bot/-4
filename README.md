Понятие дерева и графа
Определение дерева
Дерево представляет собой связный граф без циклов, включающий конечное число вершин и рёбер, между которыми существует уникальный путь. Основные характеристики дерева включают:

Наличие одной специальной вершины, называемой корнем, от которой начинаются остальные пути.
Все рёбра ориентированы от корня к остальным узлам (листьям) — вершинам, не имеющим выходящих рёбер.
Каждая вершина обладает ровно одним входящим ребром, за исключением корня, у которого нет входящих рёбер.
Примеры деревьев встречаются повсеместно, например, иерархия папок файловой системы компьютера или родословная.

Определение графа
Граф является абстрактным объектом, состоящим из набора вершин (или узлов) и связей между ними (рёбер). Графы подразделяются на:

Ориентированные (ребра имеют направления движения).
Неориентированные (нет направлений у рёбер).
Взвешенные (каждое ребро наделено весом или значением длины).
Невзвешенные (вес отсутствует).
Практическими примерами графов служат структуры социальных сетей, карты транспортных маршрутов или схем электрических цепей.

Реализация деревьев и графов на разных языках программирования
Пример реализации дерева на Python

class Node:
    def __init__(self, data):
        self.data = data
        self.children = []
    
  def append_child(self, node):
        self.children.append(node)

# Использование
tree_root = Node("Root")
child_1 = Node("Child 1")
child_2 = Node("Child 2")
tree_root.append_child(child_1)
tree_root.append_child(child_2)
Анализ: Каждый узел (Node) хранит свою информацию и список дочерних элементов. Это простой способ организации дерева, удобный для дальнейшего расширения функционала обхода и манипуляции структурой.

Пример представления графа на Java

import java.util.*;

class Vertex {
    private final String name;
    private Set adjacentVertices;

  public Vertex(String name) {
        this.name = name;
        this.adjacentVertices = new HashSet<>();
    }

  public void connectTo(Vertex other) {
        adjacentVertices.add(other);
    }

  @Override
    public boolean equals(Object obj) {
        if (!(obj instanceof Vertex)) return false;
        return ((Vertex) obj).name.equals(this.name);
    }

  @Override
    public int hashCode() {
        return Objects.hash(name);
    }
}

// Использование
Vertex v1 = new Vertex("V1");
Vertex v2 = new Vertex("V2");
v1.connectTo(v2);
v2.connectTo(v1);
Анализ: Вершина представлена классом Vertex, который поддерживает список соседних вершин. Здесь используется метод хэширования и сравнения для эффективной обработки множеств вершин.

Пример формирования графа на C++

#include <iostream>
#include <vector>
#include <unordered_set>

struct Edge {
    int from;
    int to;
};

class Graph {
private:
    std::vector<std::vector<int>> adjacency_list;

public:
    Graph(int num_vertices) : adjacency_list(num_vertices) {}

  void addEdge(const Edge& edge) {
        adjacency_list[edge.from].push_back(edge.to);
        adjacency_list[edge.to].push_back(edge.from);
    }

  const std::vector<int>& getNeighbors(int vertex_id) const {
        return adjacency_list.at(vertex_id);
    }
};

// Пример использования
int main() {
    Graph g(3);
    g.addEdge({0, 1});
    g.addEdge({1, 2});
    for (auto n : g.getNeighbors(1)) {
        std::cout << n << ' ';
    }
    return 0;
}
Анализ: Граф представлен матрицей смежности (adjacency_list), что позволяет эффективно хранить связи между вершинами. Классы обеспечивают гибкость для модификации структуры графа.

Алгоритм обхода дерева методом поиска в глубину (DFS)
Алгоритм DFS (Depth-first search) предназначен для последовательного посещения всех вершин дерева начиная с заданной начальной вершины.

Пример на Python

def depth_first_search(start_node):
    visited_nodes = set()
    traversal_stack = [start_node]

    while traversal_stack:
        current_vertex = traversal_stack.pop()
        if current_vertex not in visited_nodes:
            visited_nodes.add(current_vertex)
            print(f"Вертикаль: {current_vertex.data}")
            traversal_stack.extend(reversed(current_vertex.children))

depth_first_search(tree_root)
Описание шагов:

Начинаем с указанной стартовой вершины (start_node).
Проверяем, была ли эта вершина ранее обработана. Если нет, мы помечаем её как посещённую и обрабатываем (например, выводим её значение).
Затем последовательно добавляем в стек детей текущей вершины в обратном порядке, чтобы обеспечить нужный порядок обхода.
Повторяем процесс, пока стек не опустеет.

Оценка производительности: Каждый узел посещается лишь единожды, а каждое ребро проверяется дважды (при переходе от родительской вершины к ребёнку и обратно). Следовательно, общая временная сложность составляет O(N+M, где N — количество вершин, а M — количество рёбер.
