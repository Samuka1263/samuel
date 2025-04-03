# Criando um array de 5 posições vazias
class PersonalArray:
    SIZE = 5
    insertPosition = 0
    elements = [None] * SIZE

    def isEmpty(self):
        return self.size() == 0
    
    def size(self):
        return self.insertPosition
        
    def isMemoryFull(self):
        return self.insertPosition == len(self.elements)
    
    def append(self, newElement):
        if self.isMemoryFull():
            self.updateMemory()
        self.elements[self.insertPosition] = newElement
        self.insertPosition += 1
    
    def updateMemory(self):
        newArray = [None] * (self.size() + self.SIZE)
        for position in range(self.insertPosition):
            newArray[position] = self.elements[position]
        self.elements = newArray
    
    def clear(self):
        self.elements = [None] * self.SIZE
        self.insertPosition = 0
    
    def remove(self):
        if not self.isEmpty():
            self.elements[self.insertPosition - 1] = None
            self.insertPosition -= 1
    
    def removePosition(self, position):
        if position < 0 or position >= self.insertPosition:
            print("Posição inválida!")
            return ""
        removedElement = self.elements[position]
        index = position
        while index < self.insertPosition - 1:
            self.elements[index] = self.elements[index + 1]
            index += 1
        self.insertPosition -= 1
        return removedElement
        
    def insertAt(self, position, newElement):
        if position < 0 or position > self.insertPosition:
            print("Posição inválida!")
            return
        if self.isMemoryFull():
            self.updateMemory()
        index = self.insertPosition - 1
        while index >= position:
            self.elements[index + 1] = self.elements[index]
            index -= 1
        self.elements[position] = newElement
        self.insertPosition += 1   
        
    def elementAt(self, position):
        if position < 0 or position >= self.insertPosition:
            print("Posição inválida!")
            return None
        return self.elements[position]


# Implementação de uma fila em Python
class PersonalQueue:
    list = PersonalArray()
    
    def enqueue(self, newElement):
        self.list.insertAt(0, newElement)
    
    def dequeue(self):
        return self.list.removePosition(self.list.size() - 1)


# Sistema de Fila de Atendimento de Clientes

class AtendimentoDeClientes:
    def __init__(self):
        self.fila = PersonalQueue()

    # Função para adicionar um novo cliente à fila
    def adicionar_cliente(self, nome_cliente):
        print(f"Cliente {nome_cliente} entrou na fila.")
        self.fila.enqueue(nome_cliente)
    
    # Função para atender o próximo cliente da fila
    def atender_cliente(self):
        cliente_atendido = self.fila.dequeue()
        if cliente_atendido:
            print(f"Atendendo o cliente {cliente_atendido}...")
        else:
            print("Nenhum cliente na fila para atender!")

    # Função para mostrar os clientes na fila
    def mostrar_fila(self):
        print("Clientes na fila:")
        for i in range(self.fila.list.size()):
            print(f"- {self.fila.list.elementAt(i)}")


# Criando o sistema de atendimento
sistema_atendimento = AtendimentoDeClientes()

# Adicionando clientes à fila
sistema_atendimento.adicionar_cliente("João")
sistema_atendimento.adicionar_cliente("Maria")
sistema_atendimento.adicionar_cliente("Carlos")
sistema_atendimento.adicionar_cliente("Ana")
sistema_atendimento.adicionar_cliente("Felipe")

# Mostrando clientes na fila
sistema_atendimento.mostrar_fila()

# Atendendo os clientes na ordem correta (FIFO)
print("\nAtendendo clientes:\n")
sistema_atendimento.atender_cliente()
sistema_atendimento.atender_cliente()
sistema_atendimento.atender_cliente()
sistema_atendimento.atender_cliente()
sistema_atendimento.atender_cliente()

# Mostrando a fila após os atendimentos
print("\nFila após atendimentos:")
sistema_atendimento.mostrar_fila()

# Tentando atender um cliente quando a fila estiver vazia
print("\nTentando atender mais clientes...")
sistema_atendimento.atender_cliente()
