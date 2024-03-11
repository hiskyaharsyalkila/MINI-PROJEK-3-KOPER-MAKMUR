# MINI-PROJEK-3-KOPER-MAKMUR
HISKYA HARSYAL KILA 2309116089

~~~

class Node:
    def __init__(self, data):
        self.data = data
        self.next = None

class KoperLinkedList:
    def __init__(self):
        self.head = None
        self.tail = None

    def add_to_front(self, data):
        new_node = Node(data)
        new_node.next = self.head
        self.head = new_node
        if self.tail is None:
            self.tail = new_node

    def add_to_end(self, data):
        new_node = Node(data)
        if self.tail is None:
            self.head = new_node
            self.tail = new_node
        else:
            self.tail.next = new_node
            self.tail = new_node

    def add_after(self, prev_node, data):
        if not prev_node:
            print("Node sebelumnya tidak ditemukan!")
            return
        new_node = Node(data)
        new_node.next = prev_node.next
        prev_node.next = new_node
        if prev_node == self.tail:
            self.tail = new_node

    def delete_from_front(self):
        if self.head is None:
            print("Linked list kosong!")
            return
        self.head = self.head.next
        if self.head is None:
            self.tail = None

    def delete_from_end(self):
        if self.tail is None:
            print("Linked list kosong!")
            return
        prev_node = self.head
        while prev_node.next != self.tail:
            prev_node = prev_node.next
        prev_node.next = None
        self.tail = prev_node

    def delete_node(self, node):
        if node == self.head:
            self.delete_from_front()
            return
        prev_node = self.head
        while prev_node.next != node:
            prev_node = prev_node.next
        prev_node.next = node.next
        if node == self.tail:
            self.tail = prev_node

    def print_list(self):
        temp = self.head
        while temp:
            print(temp.data, end=" ")
            temp = temp.next
        print()

    def quick_sort(self, low, high, attribute):
        if low < high:
            pi = self.partition(low, high, attribute)
            self.quick_sort(low, pi - 1, attribute)
            self.quick_sort(pi + 1, high, attribute)

    def partition(self, low, high, attribute):
        pivot = self.get_node_by_index(low).data[attribute]
        i = low + 1
        j = high
        while i <= j:
            while i <= j and self.get_node_by_index(i).data[attribute] < pivot:
                i += 1
            while i <= j and self.get_node_by_index(j).data[attribute] >= pivot:
                j -= 1
            if i < j:
                self.swap_nodes(i, j)

        self.swap_nodes(low, j)
        return j

    def get_node_by_index(self, index):
        temp = self.head
        for i in range(index):
            temp = temp.next
        return temp

    def swap_nodes(self, i, j):
        node1 = self.get_node_by_index(i)
        node2 = self.get_node_by_index(j)
        temp = node1.data
        node1.data = node2.data
        node2.data = temp

    def sort_by_id(self, ascending=True):
        self.quick_sort(0, self.get_length() -1, "ID")
        if not ascending:
           self.reverse()

    def sort_by_nama(self, ascending=True):
        self.quick_sort(0, self.get_length() -1, "Nama")
        if not ascending:
         self.reverse()

    def get_length(self):
       count = 0
       temp = self.head
       while temp:
           count += 1
           temp = temp.next
           return count

    def reverse(self):
        prev = None
        current = self.head
        while current:
          next_node = current.next
          current.next = prev
          prev = current
          current = next_node
        self.head = prev

koper_list = KoperLinkedList()

koper1 = {"ID":11,"Nama":"Koper Baller-Silver"}
koper2 = {"ID":13,"Nama":"Koper Roaming-Hitam"}
koper3 = {"ID":15,"Nama":"Koper Lojel-Rose"}
koper4 = {"ID":17,"Nama":"Koper Airwheel-Putih"}
koper5 = {"ID":19,"Nama":"Koper Kamiliant-Rose"}

koper_list.add_to_end(koper1)
koper_list.add_to_end(koper2)
koper_list.add_to_end(koper3)
koper_list.add_to_end(koper4)
koper_list.add_to_end(koper5)

# Tampilkan daftar koper sebelum sorting
print("=======||Daftar Koper Sebelum Sorting||=======")
koper_list.print_list()

# Sorting berdasarkan ID (ascending)
koper_list.sort_by_id()

# Tampilkan daftar koper setelah sorting
print("=======||Daftar Koper Setelah Sorting berdasarkan ID||=======")
koper_list.print_list()

# Sorting berdasarkan nama (descending)
koper_list.sort_by_nama(ascending=False)

# Tampilkan daftar koper setelah sorting
print("=======||Daftar Koper Setelah Sorting berdasarkan Nama||=======")
koper_list.print_list()

~~~
