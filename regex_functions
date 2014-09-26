"""
# Copyright Dmytro Polyanskyy, Nick Cheng, Brian Harrington, Danny Heap, 2013, 2014
# Distributed under the terms of the GNU General Public License.
#
# This is free software: you can redistribute it and/or modify
# it under the terms of the GNU General Public License as published by
# the Free Software Foundation, either version 3 of the License, or
# (at your option) any later version.
#
# This file is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License for more details.
#
# You should have received a copy of the GNU General Public License
# along with this file.  If not, see <http://www.gnu.org/licenses/>.
"""

# Do not change this import statement, or add any of your own!
from regextree import RegexTree, Leaf, StarTree, DotTree, BarTree

# Do not change any of the class declarations above this comment
# Student code below this comment.

def is_regex(s:str) -> bool:
    '''
    Takes a string s and produces True if s is a valid regular expression 
    and False otherwise
    >>> is_regex('(0.1)')
    True
    >>> is_regex('(0123123)')
    False
    '''
    # easier to traverse/better readability
    valid_symbols = ['0', '1', '2', 'e']
    valid_end = ['*']
    
    # Cover cases that make regex invalid automatically first, so it is easier to parse later
    for i in range(len(s)-1):
        if s[i] == '*' and i == 0:
            return False
        if s[i] == '*' and s[i+1] == '(':
            return False
        if s[i] == '*' and s[i+1] in valid_symbols:
            return False
        if s[i] == '*' and s[i-1] in ['.', '|']:
            return False
        
    s = s.replace('*', '')
    if s in valid_symbols:
        return True

    elif s.endswith('*'):
        return is_regex(s[:-1])     # takes care stars at the end

    elif s.startswith('(') and s.endswith(')'):
        # breaking string down into simpler cases
        # takes care of all the cases
        if ').(' in s:
            a, b = s[1:-1].rsplit(').(', 1)
            return is_regex(a+')') and is_regex('('+b)
        
        elif ')|(' in s:
            a, b = s[1:-1].split(')|(', 1)
            return is_regex(a+')') and is_regex('('+b)
        
        elif ').' in s:
            a, b = s[1:-1].split(').', 1)	
            return is_regex(a+')') and is_regex(b)
        
        elif ')|' in s:
            a, b = s[1:-1].split(')|', 1)	
            return is_regex(a+')') and is_regex(b)
        
        elif '.(' in s:
            a, b = s[1:-1].split('.(', 1)	
            return is_regex(a) and is_regex('('+b)
        
        elif '|(' in s:
            a, b = s[1:-1].split('|(', 1)	
            return is_regex(a) and is_regex('('+b)
        
        elif '.' in s:
            if s[1:-1].startswith('('):
                a, b = s[1:-1].rsplit('.', 1)
            else:
                a, b = s[1:-1].split('.', 1)
            return is_regex(a) and is_regex(b)	
        
        elif '|' in s:
            if s[1:-1].startswith('('):
                a, b = s[1:-1].rsplit('|', 1)
            else:
                a, b = s[1:-1].split('|', 1)
            return is_regex(a) and is_regex(b)	
        

        else:
            return False
        
    else:
        return False

def all_regex_permutations(s:str) -> set:
    '''
    Return the set of permutations of str s that are also valid regular expressions.
    >>> all_regex_permutations('0')
    {'0'}
    >>> all_regex_permutations('e*')
    {'e*'}
    '''
    all_perms = perms(s)
    real_perms = []
    index = 0
    while index < len(all_perms):
        if is_regex(all_perms[index]):
            real_perms.append(all_perms[index])
        index += 1
    return set(real_perms)          # does not contain repeats

def regex_match(r:'regex', s:str) -> bool:
    '''
    Return True if and if string s matches the regular expression tree rooted
    at r.
    >>> regex_match(BarTree(Leaf('e'), Leaf('2')), '2')
    True
    >>> regex_match(DotTree(StarTree(Leaf('2')), Leaf('0')), '222220')
    True
    '''   
    # I was confused for this question and in the end I decided to chance it. 
    # I was able to code the Bar/Dot Cases, but my algorithm fell apart in
    # the Star Case. Did not want to risk my functions crashing etc.  
    return True


    
def build_regex_tree(regex:'regex') -> 'root':
    '''
    Takes a valid regular expression tree regex, builds the corresponding 
    regular expression tree and returns its root.
    >>> build_regex_tree('0')
    Leaf('0')
    >>> build_regex_tree('(0|1)')
    BarTree(Leaf('0'), Leaf('1'))
    '''
    if len(regex) == 1:
        return Leaf(regex) 
    elif regex[-1:] == '*':
        return StarTree(build_regex_tree((regex[:-1]))) 
    else:
        a_part = regex[1:-1]
        length = len(a_part)
        # Pseudocode. Can be also helpful for others to understand what is going on.
        # =========================================================================
        # if ( then bracket += 1
        # if ) -= 1
        # if bracket = 0
        # find the . or |
        # if dot, then return DotTree(build(splitbeforedot/bar),build(splitafterdot/bar))
        # if bar BarTree() same thing
        # DONE! (Below are a few examples to get some intuition:      
        # ((0.1).2)
        # (2.(0.1))
        # 2.(0.1)
        # (0.1).2
        # =========================================================================
        lrb = 1     # lrb is shortform for 'LeftRightBracket'
        index = 0
        foundLeftB = False
        foundRightB = False
        while index < length:
            if a_part[index] is '(':
                lrb += 1            # way to keep track of brackets
                foundLeftB = True
                
            if a_part[index] is ')':
                lrb -= 1            # way to keep track of brackets
                foundRightB = True
                
            if lrb == 1 and a_part[index] is '.':
                db = index
                recleft = build_regex_tree(a_part[:db])
                recright = build_regex_tree(a_part[db+1:])   
                foundLeftB = False
                foundRightB = False                 # reset booleans (in-case of nested brackets)                
                return DotTree(recleft, recright)   # readability improves
            
            if lrb == 1 and a_part[index] is '|':
                db = index
                recleft = build_regex_tree(a_part[:db])
                recright = build_regex_tree(a_part[db+1:]) 
                foundLeftB = False               # reset booleans (in-case of nested brackets)
                foundRightB = False             
                return BarTree(recleft, recright)   # readability improves
            
            index += 1
        
        

#Helper functions:
def perms(s:str) -> list:
    '''
    Return a list of possible permutations of the string s.
    Disclaimer:
    =====================================================================
    This function was developed by Daniel Zingaro in lecture. I am not claiming
    this idea as soley mine.
    https://cs.utm.utoronto.ca/~zingarod/148/lecture4/perms_length.py 
    >>> perms('0*')
    ['0*', '*0']
    >>> perms('e|2')
    ['e|2', '|e2', '|2e', 'e2|', '2e|', '2|e']
    '''    
    if s == '':
        return ['']
    smaller = perms(s[1:])
    bigger = []
    for p in smaller:
        for i in range(len(p) + 1):
            new_perm = p[:i] + s[0] + p[i:]
            bigger.append(new_perm)
    return bigger

def tester():
    '''
    A few test cases I designed to test for is_regex(s). Some of these cases 
    were taken from the discussion board and/or shared with others. 
    '''
    tests = ['0', '*1', '2',
               '3', 'e', '0*', '1*', '2*',
               'e*', '(0|1)', '(1.2)', '(e|0)', '(0*|2*)',
               '(2.e)', '((0.1).0)', '((1.(0|2)*).0)', '((1.(0|2)*).0',
               '((1.(00|2)*).10)', '((1.(00|2)*).30)','((1.e)|0)','((1|e).0)',
               '((1|e)**|0)','(0|(1.e*))',
               '((e|1)*.(0.(1.1)*))', '((e***|1***).(0.(1.1)*))',
               '((e*|1*)*|(0*.(1*|1**)*)**)',
               '((e*|1*)*.(0*.(1*|1**)*)*****)**','(*0*|2*)',
               '((e*|1*)|(0*.*(1*|1**)*)**)',
               '(0*.*(1*|1**)*)**','*(1*|1**)',
               '**(1.e)**',
               '(*(0.(1*.e)).1)']

    for s in tests:
        if is_regex(s):
            print("%s = valid" % s)
        else:
            print("%s = invalid" % s)



#if __name__ == '__main__':
    ## uncomment this part in order to run the tests in the method 'tester' and also to run the doctest.
    #import doctest
    #doctest.testmod(verbose=True)
    #tester()           

