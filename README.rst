++++++++++++++++++++++++++++++++++++++++
Align: polite, proper sequence alignment
++++++++++++++++++++++++++++++++++++++++

About fork
============
A fork of brentp/align that works with aligning sequences that contains non-ascii characters (useful for usage outside Bioinformatics).


Example
========

Usage example ::

    from align import aligner

    # simple equivalence matrix (every character is only matched to itself and nothing else)
    class SimpleMatrixInner:
        def __getitem__(self, y):
            if self.x == y:
                return +10
            else:
                return -10

    class MatrixWrapper:
        def __init__(self, cls): 
            self.inner = cls()

        def __getitem__(self, x):
            self.inner.x=x
            return self.inner


    print(aligner('幸福的家庭都是相似的，不幸的家庭各有各的不幸。','家庭相似', method= 'global', matrix=MatrixWrapper(SimpleMatrixInner)))
    # outputs: seq2 = '---家庭--相似--------------'

    print(aligner('幸福的家庭都是相似的，不幸的家庭各有各的不幸。','家庭相似', method= 'glocal', matrix=MatrixWrapper(SimpleMatrixInner), GAP_CHAR='#'))
    # outputs: seq2 = '家庭##相似'

    print(aligner('Все счастливые семьи похожи друг на друга, каждая несчастливая семья несчастлива по-своему.', 'несчастлива', method='global', matrix=MatrixWrapper(SimpleMatrixInner)))
    # outputs: seq2 = '---------------------------------н-----------------есчастлива------------------------------'
