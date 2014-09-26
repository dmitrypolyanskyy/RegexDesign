'''
Base_Regex is the 'Master Class'
It is the basic building block for a regex expression for the design in this file
'''
class Base_Regex():
    
    def __init__(self: 'Base_Regex', sign: str, nodes: 'list of str/int'):
        ''' 
        Initialize a Base_Regex object
        >>> b = Base_Regex('1',[])
        >>> print(b)
        Base_Regex('1', [])
        >>> b1 = Base_Regex('2',['1','2',['0','1']])
        >>> print(b1)
        Base_Regex('2', ['1', '2', ['0', '1']])
        '''
        self._sign = sign
        self._nodes = []
        length = len(nodes)
        index = 0
        while index < length:
            self._nodes.append(nodes[index])
            index += 1
            
    def __eq__(self: 'Base_Regex', other: 'Base_Regex') -> bool:
        '''
        Return True if two Base_Regex objects have the same physical structure 
        >>> b = Base_Regex('1',[])
        >>> b1 = Base_Regex('2',['1','2',['0','1']])
        >>> b == b1
        False
        '''
        if self.__repr__() == other.__repr__():
            return True
        else:
            return False        
            
    def __repr__(self: 'Base_Regex') -> str:
        """
        Returns a string which represents a Base_Regex object.
        >>> b = Base_Regex('1',[])
        >>> print(b)
        Base_Regex('1', [])
        """        
        return ('Base_Regex(' + repr(self._sign) + ', ' + repr(self._nodes) + ')') # var _sign is on the left since it has children
    

'''
These are the foundations for the classes Dot_DBN/Bar_DBN and Star_ON
The class Multiple_Nodes can be used for tree's that are not single/binary in construction. (i.e the parameter num_of_nodes should be always greater than 2
DO NOT use the foundational classes to construct Dot/Bar/Star regex signs - instead use the ones below (Dot_DBN, Bar_DBN, Star_ON)
The foundational classes however can STILL be used to construct (ONLY) custom regex signs if required.
=========================================================================================================
'''
class Double_Binary_Node(Base_Regex):
    
    def __init__(self: 'Double_Binary_Node', sign: str, child_left: 'Base_Regex', child_right: 'Base_Regex'):
        '''
        Initialize a Double_Binary_Node object
        >>> b = Base_Regex('1',[])
        >>> dbn = Double_Binary_Node('$#$', b, b)
        >>> print(dbn)
        Double_Binary_Node('$#$', Base_Regex('1', []), Base_Regex('1', []))
        '''
        Base_Regex.__init__(self, sign, [child_left, child_right]) # since Base_Regex takes a list
    
    def __eq__(self: 'Double_Binary_Node', other: 'Double_Binary_Node') -> bool:
        '''
        Return True if two Double_Binary_Node objects have the same physical structure
        >>> dbn1 = Double_Binary_Node('$#$', 1, 1)
        >>> dbn2 = Double_Binary_Node('$#$', 1, 1)
        >>> dbn1 == dbn2
        True
        '''
        if self.__repr__() == other.__repr__():
            return True
        else:
            return False    

    def __repr__(self: 'Double_Binary_Node') -> str:
        """
        Returns a string which represents a Double_Binary_Node object.
        >>> dbn1 = Double_Binary_Node('$#$', 1, 1)
        >>> print(dbn1)
        Double_Binary_Node('$#$', 1, 1)
        """           
        left_child = self._nodes[0]
        right_child = self._nodes[1]        
        return ('Double_Binary_Node('+ repr(self._sign) + ', ' + repr(left_child) + ', ' + repr(right_child) + ')')
    
        
class One_Node(Base_Regex):
    
    def __init__(self: 'One_Node', sign: str, child_node: 'Base_Regex'):
        '''
        Initialize a One_Node object
        >>> b = Base_Regex('1', [])
        >>> o = One_Node('&', b)
        >>> print(o)
        One_Node('&', Base_Regex('1', []))
        '''
        Base_Regex.__init__(self, sign, [child_node])   #since Base_Regex takes a list

    def __eq__(self: 'One_Node', other: 'One_Node') -> bool:
        '''
        Returns True if two One_Node objects have the same physical structure
        >>> b = Base_Regex('1', [])
        >>> o = One_Node('%', b)
        >>> o1 = One_Node('$', b)
        >>> o == o1
        False
        '''        
        if self.__repr__() == other.__repr__():
            return True
        else:
            return False  
        
    def __repr__(self: 'One_Node') -> str:
        """
        Returns a string which represents a One_Node object.
        >>> b = Base_Regex('1', [])
        >>> o = One_Node('@', b)
        >>> print(o)
        One_Node('@', Base_Regex('1', []))
        """           
        only_child = self._nodes[0]
        return 'One_Node('  + repr(self._sign) + ', ' + repr(only_child) + ')'
    
        
class Multiple_Nodes(Base_Regex):
    
    def __init__(self: 'Multiple_Nodes', sign: 'str', num_of_nodes: 'int'):
        '''
        Initialize a Multipe_Nodes object.
        '''
        index = 0 
        self.nodes1 = []
        while index < num_of_nodes:
            nodez = input('Please enter a child value: ')
            self.nodes1.append([nodez])
            index += 1
        Base_Regex.__init__(self, sign, [self.nodes1])
        
    def __eq__(self: 'Multiple_Nodes', other: 'Multiple_Nodes') -> bool:
        '''
        Returns True if two Multiple_Node objects have the same physical structure
        '''        
        if self.__repr__() == other.__repr__():
            return True
        else:
            return False    
        
    def __repr__(self: 'Multiple_Nodes') -> str:
        """
        Returns a string which represents a Multiple_Nodes object.
        """           
        length = len(self.nodes1)
        mult_child = []
        count = 0
        while count < length:
            mult_child.append(self.nodes1[count])
            count += 1
        return 'Multiple_Nodes('  + repr(self._sign) + ', ' + repr(mult_child) + ')'  
     
        
          

'''
End of Foundational classes
=========================================================================================================
Beginning of Dot/Bar/Star classes! These classes inherit from more general (foundational) classes. Use these to make explicit Dot/Bar/Star objects
'''

class Dot_DBN(Double_Binary_Node):
    
    def __init__(self: 'Dot_DBN', child_left: 'Base_Regex', child_right: 'Base_Regex'):
        '''
        Initialize a Dot_DBN object
        >>> d = Dot_DBN('1', '1')
        >>> print(d)
        Dot_DBN('1', '1')
        '''
        Double_Binary_Node.__init__(self, '.', child_left, child_right)
       
    def __eq__(self: 'Dot_DBN', other: 'Dot_DBN') -> bool:
        '''
        Returns True if two Dot_DBN objects have the same physical structure
        >>> d = Dot_DBN('1', '1')
        >>> d1 = Dot_DBN('1', ['2'])
        >>> d == d1
        False
        '''        
        if self.__repr__() == other.__repr__():
            return True
        else:
            return False 
        
    def __repr__(self: 'Dot_DBN') -> str:
        """
        Returns a string which represents a Dot_DBN object.
        >>> d1 = Dot_DBN('1', ['2'])
        >>> print(d1)
        Dot_DBN('1', ['2'])
        """           
        left_child = self._nodes[0]
        right_child = self._nodes[1]
        return 'Dot_DBN('+ repr(left_child) + ', ' + repr(right_child) +')' 
       
    
class Bar_DBN(Double_Binary_Node):
    
    def __init__(self: 'Bar_DBN', child_left: 'Base_Regex', child_right: 'Base_Regex'):
        '''
        Initialize a Bar_DBN object
        >>> b = Bar_DBN('1', '1')
        >>> print(b)
        Bar_DBN('1', '1')
        '''
        Double_Binary_Node.__init__(self, '|', child_left, child_right) # initializes as list already
        
    def __eq__(self: 'Bar_DBN', other: 'Bar_DBN') -> bool:
        '''
        Returns True if two Bar_DBN objects have the same physical structure
        >>> b = Bar_DBN('1', '1')
        >>> b1 = Bar_DBN('1', ['2'])
        >>> b == b1
        False
        '''        
        if self.__repr__() == other.__repr__():
            return True
        else:
            return False  
        
    def __repr__(self: 'Bar_DBN') -> str:
        """
        Returns a string which represents a Bar_DBN object.
        >>> b1 = Bar_DBN('1', ['2', '3'])
        >>> print(b1)
        Bar_DBN('1', ['2', '3'])
        """           
        left_child = self._nodes[0]
        right_child = self._nodes[1]        
        return 'Bar_DBN('+ repr(left_child) + ', ' + repr(right_child) +')'
    
class Star_ON(One_Node):
    
    def __init__(self: 'Star_ON', child_nodes: 'Base_Regex'):
        '''
        Initialize a Star_ON object
        >>> b = Base_Regex('1', [])
        >>> s = Star_ON(b)
        >>> print(s)
        Star_ON(Base_Regex('1', []))
        '''
        One_Node.__init__(self, '*', child_nodes)   # initializes as list already
        
    def __eq__(self: 'Star_ON', other: 'Star_ON') -> bool:
        '''
        Returns True if two Star_ON objects have the same physical structure
        >>> s1 = Star_ON(['1', []])
        >>> s2 = Star_ON(['2', ['1', '3']])
        >>> s1 == s2
        False
        '''        
        if self.__repr__() == other.__repr__():
            return True
        else:
            return False   
        
    def __repr__(self: 'Star_ON') -> str:
        """
        Returns a string which represents a Star_ON object.
        >>> s2 = Star_ON(['2', ['1', '3']])
        >>> print(s2)
        Star_ON(['2', ['1', '3']])
        """           
        only_child = self._nodes[0]
        return 'Star_ON(' + repr(only_child) + ')' 
    
    

if __name__ == '__main__':
    print('==========================================================================================')
    print('Hello, here are some extra directions: (more can be found within the docstrings)')
    print('Base_Regex is the master class and it is used to build up to a regex expression')
    print('Double_Binary_Node, One_Node and Multiple_Nodes are only used to build custom regex expressions')
    print('Do not use them to make Bar, Dot and Star nodes - instead use Bar_DBN, Dot_DBN, Star_ON classes only!')
    print('Use Multiple_Nodes when you have more than 2 children (i.e paramater num_of_nodes has to be greater than 2)')
    print('Please use the examples in the docstrings to understand further how to utilize the design interface')
    print('==========================================================================================')
    
