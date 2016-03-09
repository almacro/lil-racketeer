    ;;; chapter 1, Toys

    ; is it true that this is an atom? 'atom
    ;; yes, because atom is a string of characters beginning with the letter a.
    (atom? 'atom)

    ; is it true that this is an atom? 'turkey
    ;; yes, because turkey is a string of characters beginning with a letter.
    (atom? 'turkey)

    ; is it true that this is an atom? 1492
    ;; yes, because 1492 is a string of characters beginning with a digit.
    (atom? 1492)

    ; is it true that this is an atom? '3turkeys
    ;; yes, because 3turkeys is a string of characters beginning with a digit.
    (atom? '3turkeys)

    ; is it true that this is an atom? 'u
    ;; yes, because u is a string of one character beginning with a letter or digit.
    (atom? 'u)

    ; is it true that this is an atom? '*abc$
    ;; yes, because *abc$ is a string of characters beginning with a letter, digit,
    ;; or special character other than a left "("  or right ")" paranthesis.
    (atom? '*abc$)

    ; is it true that this is a list? '(atom)
    ;; yes, because (atom) is an atom enclosed by parantheses.
    (list? '(atom))

    ; is it true that this is a list? '(atom turkey or)
    ;; yes, because it is a collection of atoms enclosed by parantheses.
    (list? '(atom turkey or))

    ; is it true that this is a list? '(atom turkey) or
    ;; no, since this is actually two S-expressions not enclosed by parantheses.
    ;; The first one is a list containing two atoms, and the second one is an atom.
    ;  (list? '(atom turkey) or) -> ERROR or: bad syntax in: or

    ; is it true that this is a list? '((atom turkey) or)
    ;; yes, because the two S-expressions are now enclosed by parantheses.
    (list? '((atom turkey) or))

    ; is it true that this is an S-expression? xyz
    ;; yes, because all atoms are S-expressions.
    'xyz

    ; is it true that this is an S-expression? '(x y z)
    ;; yes, because it is a list.
    '(x y z)

    ; is it true that this is an S-expression? '((x y) z)
    ;; yes, because all lists are S-expressions.
    '((x y) z)

    ; is it true that this is a list? '(how are you doing so far)
    ;; yes, because it is a collection of S-expressions enclosed by parantheses.
    (list? '(how are you doing so far))

    ; how many S-expressions are in the list '(how are you doing so far)
    ; and what are they?
    ;; Six: how, are, you, doing, so and for.

    ; is it true that this is a list? '(((how) are) ((you) (doing so)) far)
    ;; yes, because it is a collection of S-expressions enclosed by parantheses.
    (list? '(((how) are) ((you) (doing so)) far))

    ; how many S-expressions are in the list: '(((how) are) ((you) (doing so)) far)
    ; and what are they?
    ;; Three, ((how) are), ((you) (doing so)) and far

    ; is it true that this is a list? '()
    ;; yes, because it contains zero S-expressions enclosed by parantheses.
    ;; this special S-expression is called the null list.
    (list? '())

    ; is it true that this is an atom? '()
    ;; yes, because '() is both a list and an atom.
    (atom? '())

    ; is it true that this is a list? '(() () () ())
    ;; yes, because it is a collection of s-expressions enclosed by parantheses.
    (list? '(() () () ()))

    ; what is the car of l, where l is the argument '(a b c)
    ;; 'a, because 'a is the first atom of this list.
    (let ((l '(a b c)))
      (car l))

    ; what is the car of l, where l is the argument '((a b c) x y z)
    ;; '(a b c), because '(a b c) is the first S-expression of this non-null list.
    (let ((l '((a b c) x y z)))
      (car l))

    ; what is the car of l, where l is the argument hotdog
    ;; no answer. you cannot ask for the car of an atom.
    ; (car 'hotdog) -> car contract violation, expected: pair?, given: 'hotdog

    ; what is the car of l, where  l is the argument '()
    ;; no answer. you cannot ask for the car of an atom.
    ; (car '()) -> car contract violation, expected: pair?, given: '()


    #|
    The Law of Car

    Car is defined only for non-null lists. 
    |#


    ; what is the car of l, where l is the argument '(((hotdogs)) (and) (pickle) relish)
    ;; '((hotdogs)), read as "The list of list of 'hotdogs." '((hotdogs)) is the first S-expression of l.
    (let ((l '(((hotdogs)) (and) (pickle) relish))) (car l))

    ; what is (car l), where l is the argument '(((hotdogs)) (and) (pickle) relish)
    ;; '((hotdogs)), because (car l) is another way to ask for "the car of the list l."

    ; what is (car (car l)), where l is the argument '(((hotdogs)) (and))
    ;; '(hotdogs)
    (let ((l '(((hotdogs)) (and)))) (car (car l)))

    ; what is the cdr of l, where l is the argument '(a b c)
    ;; '(b c), because '(b c) is the list l, without (car l).
    (let ((l '(a b c))) (cdr l))

    ; what is the cdr of l, where l is the argument '((a b c) x y z)
    ;; '(x y z)
    (let ((l '((a b c) x y z))) (cdr l))

    ; what is (cdr l), where l is the argument '((x) t r)
    ;; '(t r), because (cdr l) is just another way to ask for "the cdr of the list l."
    (let ((l '((x) t r))) (cdr l))


    ; what is (cdr a), where a is the argument hotdogs
    ;; no answer. you cannot ask for the cdr of an atom.
    ; (let ((a 'hotdogs)) (cdr a)) -> cdr: contract violation, expected: pair?, given 'hotdogs

    ; what is (cdr l), where l is the argument '()
    ;; no answer. you cannot ask for the cdr of the null list.
    ; (let ((l '())) (cdr l)) -> cdr: contract violation, expected: pair?, given '()


    #|
    The Law of Cdr

    Cdr is defined only for non-null lists.
    The cdr of any non-null list is always another list.
    |#


    ; what is (car (cdr l)), where l is the argument '((b) (x y) ((c)))
    ;; '(x y), because '((x y) ((c))) is (cdr l), and '(x y) is the car of (cdr l)
    (let ((l '((b) (x y) ((c))))) (car (cdr l)))

    ; what is (cdr (cdr l)), where l is the argument '((b) (x y) ((c)))
    ;; '(((c))), because '((x y) ((c))) is (cdr l), and '(((c))) is the cdr of (cdr l)Ω(let ((l '((b) (x y) ((c))))) (cdr (cdr l)))

    ; what is (cdr (car l)), where l is the argument '(a (b (c)) d)
    ;; no answer, since (car l) is an atom, and cdr does not take an atom for an argument;
    ;; see The Law of Cdr
    ;(let ((l '(a (b (c)) d))) (cdr (car l))) -> cdr: contract violation, expected: pair, given 'a

    ; what does car take as an argument?
    ;; it takes any non-null list as its argument.

    ; what does cdr take as an argument?
    ;; it takes any non-null list as its argument.

    ; what is the cons of the atom a and the list l, where
    ;    a is the argument peanut, and
    ;    l is the argument (butter and jelly), and
    ; This can also be written "(cons a l)."
    ;    Read: "cons the atom a onto the list l."
    ;; '(peanut butter and jelly)
    (let ((a 'peanut)
          (l '(butter and jelly)))
      (cons a l))

    ; what is the cons of s and l, where
    ;   s is '(mayonnaise and), and
    ;   l is '(peanut butter and jelly)
    ;; '((mayonnaise and) peanut butter and jelly)
    (let ((s '(mayonnaise and))
          (l '(peanut butter and jelly)))
      (cons s l))

    ; what is (cons s l), where
    ;   s is '((help) this), and
    ;   l is '(is very ((hard) to learn))
    ;; '(((help) this) is very ((hard) to learn))
    (let ((s '((help) this))
          (l '(is very ((hard) to learn))))
      (cons s l))

    ; what does cons take as its arguments?
    ;; cons takes two arguments:
    ;;    the first one is any S-expression;
    ;;    the second one is any list.

    ; what is (cons s l), where
    ;    s is '(a b (c)), and
    ;    l is ()
    ;; '((a b (c)))
    (let ((s '(a b (c)))
          (l '()))
      (cons s l))

    ; what is (cons s l), where
    ;    s is 'a, and
    ;    l is '()
    ;; '(a)
    (let ((s 'a)
          (l '()))
      (cons s l))

    ; what is (cons s l), where
    ;    s is '(a b (c)), and
    ;    l is 'b
    ;; '((a b (c)) . b)  (NOTE: we get the same answer in Common Lisp [clozure])
    ;; AS PUBLISHED: no answer, since the second argument l must be a list
    (let ((s '(a b (c)))
          (l 'b))
      (cons s l))

    ; what is (cons s l), where
    ;    s is 'a, and
    ;    l is 'b
    ;; '(a . b)          (NOTE: we get the same answer in Common Lisp [clozure])
    ;; AS PUBLISHED: no answer, why?
    (let ((s 'a)
          (l 'b))
      (cons s l))


    #|
    The Law of Cons

    Cons takes two arguments.
    The second argument of cons must be a list.
    The result is a list.
    |#


    ; what is (cons s (car l)), where
    ;    s is 'a, and
    ;    l is ((b) c d)
    ;; '(a b)
    (let ((s 'a)
          (l '((b) c d)))
      (cons s (car l)))

    ; what is (cons s (cdr l)), where
    ;    s is 'a, and
    ;    l is ((b) c d)
    ;; '(a c d)
    (let ((s 'a)
          (l '((b) c d)))
      (cons s (cdr l)))

    ; is it true that the list l is the null list,
    ;   where l is '()?
    ; this question can also be written:
    ;   (null? l)
    ;; #t, because it is the list composed of zero S-expressions
    (let ((l '()))
      (null? l))

    ; what is (null? (quote ()))
    ;; #t, because (quote ()) is a way of expressing the null list.
    (null? (quote ()))

    ; is (null? l) true or false, where l is the argument '(a b c)
    ;; #f, because it is a non-null list.
    (let ((l '(a b c)))
      (null? l))

    ; is (null? a) true or false, where a is 'spaghetti
    ;; #f                (NOTE: we get NIL in Common Lisp [clozure])
    ;; AS PUBLISHED: no answer, because you cannot ask null? of a non-null atom
    (let ((a 'spaghetti))
      (null? a))


    #|
    The Law of Null?

    Null? is defined only for lists.
    |#


    ; is it true or false, that s is an atom, where s is 'Harry
    ;; #t, because 'Harry is a string of characters beginning with a letter.
    (let ((s 'Harry))
      (atom? s))

    ; is (atom? s), true or false, where s is 'Harry
    ;; #t, because (atom? s) is just another way to ask,
    ;;   "Is it true or false that s is an atom?"
    (let ((s 'Harry))
      (atom? s))

    ; is (atom? s) true or false, where s is '(Harry had a heap of apples)
    ;; #f, since the argument s is a list.
    (let ((s '(Harry had a heap of apples)))
      (atom? s))

    ; how many arguments does (atom?) take, and what are they?
    ;; it takes one argument. the argument can be any S-expression.

    ; is (atom? (car l)) true or false, where l is '(Harry had a heap of apples)
    ;; #t, because (car l) is 'Harry, and 'Harry is an atom.
    (let ((l '(Harry had a heap of apples)))
      (atom? (car l)))

    ; is (atom? (cdr l)) true or false, where l is '(Harry had a heap of apples)
    ;; #f
    (let ((l '(Harry had a heap of apples)))
      (atom? (cdr l)))

    ; is (atom? (cdr l)) true or false, where l is '(Harry)
    ;; #t, because the list '() is also an atom
    (let ((l '(Harry)))
      (atom? (cdr l)))

    ; is (atom? (car (cdr l))) true or false, where l is (swing low sweet cherry)
    ;; #t, because (cdr l) is '(low sweet cherry), and (car (cdr l)) is low, which is an atom.
    (let ((l '(swing low sweet cherry)))
      (atom? (car (cdr l))))

    ; is (atom? (car (cdr l))) true or false, where l is (swing (low sweet) cherry)
    ;; #f, since (cdr l) is '((low sweet) cherry), and (car (cdr l)) is '(low sweet), which is a list.
    (let ((l '(swing (low sweet) cherry)))
      (atom? (car (cdr l))))

    ; true or false: a1 and a2 are the same atom, where
    ;    a1 is 'Harry, and
    ;    a2 is 'Harry
    ;; #t, because a1 is the atom 'Harry and a2 is the the atom 'Harry
    (let ((a1 'Harry)
          (a2 'Harry))
      (eq? a1 a2))

    ; is (eq? a1 a2) true or false, where
    ;    a1 is the argument 'Harry, and
    ;    a2 is the argument 'Harry
    ;; #t, because (eq? 'a1 'a2) is just another way to ask "are a1 and a2 the same atom?"
    (let ((a1 'Harry)
          (a2 'Harry))
      (eq? a1 a2))

    ; is (eq? a1 a2) true or false, where
    ;     a1 is 'margarine, and
    ;     a2 is 'butter
    ;; #f, since the a1 and a2 are different atoms.
    (let ((a1 'margarine)
          (a2 'butter))
      (eq? a1 a2))

    ; how many arguments does eq? take, and what are they?
    ;; it takes two arguments. both of them must be atoms.

    ; is (eq? l1 l2) true or false, where
    ;    l1 is '() and
    ;    l2 is '(strawberry)
    ;; #f                [NOTE: we get NIL in Common Lisp [clozure] from (eq '() '(strawberry))]
    ;; AS PUBLISHED: no answer, although '() is an atom, '(strawberry) is a non-null list.
    (let ((l1 '())
          (l2 '(strawberry)))
      (eq? l1 l2))


    #|
    The Law of Eq?

    Eq? takes two arguments.
    Each must be an atom.
    |#


    ; is (eq? (car l) a) true or false, where
    ;    l is '(Mary had a little lamb chop), and
    ;    a is 'Mary
    ;; #t, because (car l) is the atom 'Mary,
    ;;   and the argument a is also the atom 'Mary.
    (let ((l '(Mary had a little lamb chop))
          (a 'Mary))
      (eq? (car l) a))

    ; is (eq? (cdr l) a) true or false, where
    ;    l is '(soured milk), and
    ;    a is 'milk
    ;; #f                [NOTE: we get NIL in Common Lisp [clozure] from (eq (cdr '(soured milk)) 'milk)]
    ;; AS PUBLISHED: no answer. see the laws of Cdr and Eq?
    (let ((l '(soured milk))
          (a 'milk))
      (eq? (cdr l) a))

    ; is (eq? (car l) (car (cdr l))) true or false, where
    ;    l is '(beans beans we need jelly beans)
    ;; #t, as this compares the first and second atoms in the list.
    (let ((l '(beans beans we need jelly beans)))
      (eq? (car l) (car (cdr l))))


    ;;; exercises, chapter 1

    ; 1.1 think of 10 different atoms and write them down
    21
    "hi there"
    44.4
    'milky-way
    'martin
    'day-after-tomorrow
    0.0001
    3.14159
    2.72
    3/4

    ; 1.2 using the atoms of exercise 1.1, make up twenty different lists
    '("hi there" 21)
    '(21 "hi there")
    '(martin day-after-tomorrow)
    '(2.72 3.14159 0.0001)
    '(2.72 0.0001 3.14159)
    '(0.0001 2.72 3.14159)
    '(0.0001 3.14159 2.72)
    '(martin 3/4)
    '(3/4 milky-way 21)
    '(21 milky-way 3/4)
    '(milky-way 21 3/4)
    '(3/4 21 milky-way)
    '(martin (martin) ((martin)))
    '(0.0001 0.0001 0.0001 0.0001 0.0001)
    '("hi there" martin)
    '(martin "hi there")
    '(21 44.4)
    '(2.72 44.4 0.0001 3.14159)
    '(21 day-after-tomorrow)
    '(martin day-after-tomorrow)

    ; 1.3 the list '(all these problems) can be constructed by (cons a (cons b (cons c d))), where
    ;    a is 'all
    ;    b is 'these
    ;    c is 'problems, and
    ;    d is '()
    ;  how would you construct the following lists:
    ;    (all (these problems))
    (let ((a 'all)
          (b 'these)
          (c 'problems)
          (d '()))
      (cons a (cons (cons b (cons c d)) d)))
    ;     (all (these) problems)
    (let ((a 'all)
          (b 'these)
          (c 'problems)
          (d '()))
      (cons a (cons (cons b d) (cons c d))))
    ;     ((all these) problems)
    (let ((a 'all)
          (b 'these)
          (c 'problems)
          (d '()))
      (cons (cons a (cons b d)) (cons c d)))
    ;     ((all these problems))
    (let ((a 'all)
          (b 'these)
          (c 'problems)
          (d '()))
      (cons (cons a (cons b (cons c d))) d))

    ; 1.4 what is (car (cons a l)), where a is 'french and l is '(fries)
    (let ((a 'french)
          (l 'fries))
      (car (cons a l)))

    'french
    ; what is (cdr (cons a l)), where a is 'oranges and l is '(apples and peaches)
    (let ((a 'oranges)
          (l '(apples and peaches)))
      (cdr (cons a l)))

    '(apples and peaches)

    ; 1.5 find an atom x that makes (eq? x y) true, where y is 'lisp. are there any others
    (let ((x 'lisp) (y 'lisp)) (eq? x y))

    ; 1.6 if a is atom, is there a list l that makes (null? (cons a l)) true?
    #f

    ; 1.7 determine the value
    ; (cons s l), where 's is 'x and l is 'y
    (let ((s 'x)
          (l 'y))
      (cons s l))
    ;; '(x . y)

    ; (cons s l), where 's is '() and l is '()
    (let ((s '())
          (l '()))
      (cons s l))
    ;; '(())

    ; (car s), where s is '()
    ;; no answer -> car: contract violation, expected: pair?, given: '()

    ; (cdr l), where l is '(())
    (let ((l '(())))
      (cdr l))
    ;; '()

    ; 1.8 true or false
    ; (atom? (car l)), where l is '((meatballs) and spaghetti)
    (let ((l '((meatballs) and spaghetti)))
      (atom? (car l)))
    ;; #f

    ; (null? (cdr l)), where l is '((meatballs))
    (let ((l '((meatballs))))
      (null? (cdr l)))
    ;; #t

    ; (eq? (car l) (car (cdr l))), where l is '(two meatballs)
    (let ((l '(two meatballs)))
      (eq? (car l) (car (cdr l))))
    ;; #f

    ; (atom? (cons a l)), where l is '(ball) and a is 'meat
    (let ((l '(ball)) (a 'meat))
      (atom? (cons a l)))
    ;; #f

    ; 1.9 what is
    ; (car (cdr (cdr (car l)))), where l is '((kiwis mangoes lemons) and (more))
    (let ((l '((kiwis mangoes lemons) and (more))))
      (car (cdr (cdr (car l)))))
    ;; 'lemons

    ; (car (cdr (car (cdr l)))), where l is '(() (eggs and (bacon)) (for) (breakfast))
    (let ((l '(() (eggs and (bacon)) (for) (breakfast))))
      (car (cdr (car (cdr l)))))
    ;; 'and

    ; (car (cdr (cdr (cdr l)))), where l is '(() () () (and (coffee)) please)
    (let ((l '(() () () (and (coffee)) please)))
      (car (cdr (cdr (cdr l)))))
    ;; '(and (coffee))

    ; 1.10 to get the atom 'and in '(peanut butter and jelly on toast), we can write (car (cdr (cdr l)))
    ;        what would you write to get
    ;  'Harry in l, where l is '(apples in (Harry has a backyard))
    (let ((l '(apples in (Harry has a backyard))))
      (car (car (cdr (cdr l)))))

    ;               where l is '(apples and Harry)
    (let ((l '(apples and Harry)))
      (car (cdr (cdr l))))

    ;               where l is '(((apples) and ((Harry))) in his backyard)
    (let ((l '(((apples) and ((Harry))) in his backyard)))
      (car (car (car (cdr (cdr (car l)))))))

