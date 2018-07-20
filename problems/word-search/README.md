
# Leetcode: Word Search     :BLOG:Hard:

---

Word Search  

---

Similar Problems:  

-   Tag: [#codetemplate](https://code.dennyzhang.com/tag/codetemplate)

---

Given a 2D board and a word, find if the word exists in the grid.  

The word can be constructed from letters of sequentially adjacent cell, where "adjacent" cells are those horizontally or vertically neighboring. The same letter cell may not be used more than once.  

For example,  

    Given board =
    
    [
      ['A','B','C','E'],
      ['S','F','C','S'],
      ['A','D','E','E']
    ]
    word = "ABCCED", -> returns true,
    word = "SEE", -> returns true,
    word = "ABCB", -> returns false.

Github: [challenges-leetcode-interesting](https://github.com/DennyZhang/challenges-leetcode-interesting/tree/master/problems/word-search)  

Credits To: [leetcode.com](https://leetcode.com/problems/word-search/description/)  

Leave me comments, if you have better ways to solve.  

---

    ## Blog link: https://code.dennyzhang.com/word-search
    ## Basic Ideas: backtracking
    ##
    ## Complexity: Time ?, Space ?
    class Solution(object):
        def exist(self, board, word):
    	"""
    	:type board: List[List[str]]
    	:type word: str
    	:rtype: bool
    	"""
    	word_len = len(word)
    	if word_len == 0: return True
    
    	self.row_count = len(board)
    	if self.row_count == 0: return False
    	self.col_count = len(board[0])
    
    	l = []
    	for i in xrange(self.row_count):
    	    for j in xrange(self.col_count):
    		if board[i][j] == word[0]:
    		    if word_len == 1: return True
    		    l.append((i, j))
    		    if self.myExist(board, i, j, l, word[1:]):
    			return True
    		    else:
    			l.pop()
    	return False
    
        def myExist(self, board, i, j, l, word):
    	if len(word) == 0: return True
    	# check the neighbors of board[i][j]
    	for (ik, jk) in [(-1, 0), (1, 0), (0, -1), (0, 1)]:
    	    i2, j2 = i+ik, j+jk
    	    if i2<0 or i2>=self.row_count or j2<0 or j2>=self.col_count:
    		continue
    	    if board[i2][j2] != word[0] or (i2, j2) in l:
    		continue
    	    # go deeper with this direction
    	    l.append((i2, j2))
    	    if self.myExist(board, i2, j2, l, word[1:]):
    		return True
    	    else:
    		# restore context
    		l.pop()
    	return False
    
    # s = Solution()
    # print s.exist([["A","B","C","E"],["S","F","E","S"],["A","D","E","E"]], "ABCESEEEFS") # True
    # print s.exist([["C","A","A"],["A","A","A"],["B","C","D"]], "AAB") # true
