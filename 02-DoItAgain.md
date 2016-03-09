
    ;;; chapter 2, Do It, Do It Again, and Again, and Again

    ; true or false: (lat? l), where l is '(Jack Sprat could eat no chicken fat)
    ;; true, because each S-expression in l is an atom

    ; true or false: (lat? l), where l is '((Jack) Sprat could eat no chicken fat)
    ;; false, since (car l) is a list

    ; true or false: (lat? l), where l is '(Jack (Sprat could) eat no chicken fat)
    ;; false, since one of the S-expressions in l is a list

    ; true or false: (lat? l), where l is '()
    ;; true, because '() contains no lists, and because it does not contain any lists, it is a lat

    ; true or false: a lat is a list of atoms
    ;; every lat is a list of atoms!

    ; write the function lat? using some, but not necessarily all of the following functions:
    ;   car, cdr, cons, null?, atom?, and eq?
    ;; we do not expect you to know this, because you are still missing some ingredients.
    ;; go on to the next question. good luck.
    (define (lat? l)  ; my version
      (cond ((null? l) #t)
            ((atom? (car l)) (lat? (cdr l)))
            (else #f)))

    ; what is the value of (lat? l), where l is the argument '(bacon and eggs)
    ;(define lat?      ; book's version, tweaked for racket/scheme
    ;  (lambda (l)
    ;    (cond
    ;      ((null? l) #t)
    ;      ((atom? (car l)) (lat? (cdr l)))
    ;      (#t #f))))
    ;; the application (lat? l), where l is '(bacon and eggs)
    ;;   has the value #t -- true -- because l is a lat.

    ; how do you determine the answer #t for the application
    ;    (lat? l)
    ;; we did not expect you to know this one either.
    ;; the answer is determined by answering the questions asked by lat?
    ;;    hint: write down the function lat? and refer to it for the next group of questions

    ; what is the first question asked by lat?
    ;; (null? l)
    ;;    note: (cond ...) is the one that asks questions;
    ;;          (lambda ...) creates a function;
    ;;          and (define ...) gives it a name.

    ; what is the meaning of the cond-line
    ;    ((null? l) #t)
    ; where
    ;    l is '(bacon and eggs)
    ;; (null? l) asks if the argument l is the null list.
    ;; if it is, then the value of the application is true.
    ;; if it is not, then we ask the next question.
    ;; in this case, l is not the null list, so we ask the next question.

    ; what is the next question?
    ;; (atom? (car l))

    ; what is the meaning of the line
    ;    ((atom? (car l)) (lat? (cdr l)))
    ; where
    ;    l is '(bacon and eggs)
    ;; (atom? (car l)) asks if the first S-expression of the list l is an atom.
    ;; if (car l) is an atom, then we want to know if the rest of l is also composed
    ;; only of atoms. if (car l) is not an atom, then we ask the next question.
    ;; in this case, (car l) is an atom, so the value of the function is the value
    ;; of (lat? (cdr l)).

    ; what is the meaning of
    ;    (lat? (cdr l))
    ;; (lat? (cdr l)) finds out if the rest of the list l is composed only of
    ;; atoms, by referring to the function, but now with a new argument.

    ; now, what is the argument l for lat?
    ;; now the argument l is (cdr l), which is
    ;;    '(and eggs)

    ; what is the next question?
    ;; (null? l)

    ; what is the meaning of the line
    ;    ((null? l) #t)
    ; where
    ;    l is now '(and eggs)
    ;; (null? l) asks if the argument l is the null list.
    ;; if it is, then the value of the application is #t.
    ;; if it is not, then we ask the next question.
    ;; in this case, l is not the null list, so we ask the next question.

    ; what is the next question?
    ;; (atom? (car l))

    ; what is the meaning of the line
    ;    ((atom? (car l)) (lat? (cdr l)))
    ; where
    ;    l is '(and eggs)
    ;; (atom? (car l)) asks if the (car l) is an atom.
    ;; if it is an atom, then the value of the application is
    ;; (lat? (cdr l)). if not, then we ask the next question.
    ;; in this case, (car l) is an atom, so we want to find out if
    ;; the rest of the list is composed only of atoms.

    ; what is the meaning of
    ;    (lat? (cdr l))
    ;; (lat? (cdr l)) finds out if the rest of l is composed
    ;; only of atoms, by referring again to the function lat?
    ;; but this time, with the argument (cdr l), which is '(eggs)

    ; what is the next question?
    ;; (null? l)

    ; what is the meaning of the line
    ;    ((null? l) t)
    ; where
    ;    l is now '(eggs)
    ;; (null? l) asks if the argument l is the null list.
    ;; if it is, the value of the application is #t, namely true.
    ;; if it is not, then move to the next question. in this case,
    ;; l is not null, so we ask the next question.

    ; what is the next question?
    ;; (atom? (car l))

    ; what is the meaning of the line
    ;    ((atom? (car l)) (lat? (cdr l)))
    ; where
    ;    l is now '(eggs)
    ;; (atom? (car l)) asks if (car l) is an atom. if it is,
    ;; then the value of the application is (lat? (cdr l)).
    ;; if (car l) is not an atom, then ask the next question.
    ;; in this case, (car l) is an atom, so once again we
    ;; look at (lat? (cdr l))

    ; what is the meaning of (lat? (cdr l))
    ;; (lat? (cdr l)) finds out if the rest of the list l is
    ;; composed only of atoms, by referring to the function lat?
    ;; with l becoming the value of (cdr l)

    ; now, what is the argument for lat?]
    ;; '()

    ; what is the meaning of the line
    ;    ((null? l) #t)
    ; where
    ;    l is now '()
    ;; (null? l) asks if the argument l is the null list.
    ;; if it is, then the value of the application is the value #t.
    ;; if not, then we ask the next question. in this case,
    ;; '() is the null list. therefore, the value of the
    ;; application (lat? l), where l is '(bacon and eggs), is #t -- true.

    ; do you remember the question about
    ;    (lat? l)
    ;; probably not. the application (lat? l) has a value #t
    ;; if the list l is a list of atoms, where l is '(bacon and eggs)

    ; can you describe what the function lat?
    ; does in your own words?
    ;; here are our words:
    ;;  "lat? looks at each S-expression, in turn,
    ;;   and asks if each S-expression is an atom,
    ;;   until it runs out of S-expressions. if it
    ;;   runs out without encountering a list, the
    ;;   value of #t. if it finds a list, the value
    ;;   is #f -- false."
    ;; to see how we could arrive at a value of
    ;; "false," consider the next few questions.

    ; this is the function lat?, again:
    ;(define lat?      ; book's version, tweaked for racket/scheme
    ;  (lambda (l)
    ;    (cond
    ;      ((null? l) #t)
    ;      ((atom? (car l)) (lat? (cdr l)))
    ;      (#t #f))))
    ; what is the value of (lat? l), where
    ;    l is now '(bacon (and eggs))
    ;; #f
    ;;  since the list l contains an S-expression that is a list.

    ; what is the first question?
    ;; (null? l)

    ; what is the meaning of the line
    ;    ((null? l) #t)
    ; where
    ;    l is '(bacon (and eggs))
    ;; (null? l) asks if l is the null list. if it is, the
    ;; value is #t. if l is not null, then move to the next
    ;; question. in this case, it is not null, so we ask the
    ;; next question.

    ; what is the next question?
    ;; (atom? (car l))

    ; what is the meaning of the line
    ;    ((atom? (car l)) (lat? (cdr l)))
    ; where
    ;    l is (bacon (and eggs))
    ;; (atom? (car l)) asks if (car l) is an atom. if it is,
    ;; the value is (lat? (cdr l)). if it is not, we ask the
    ;; next question. in this case, (car l) is an atom, so
    ;; we want to check if the rest of the list l is composed
    ;; only of atoms.

    ; what is the meaning of
    ;    (lat? (cdr l))
    ;; (lat? (cdr l)) checks to see if the rest of the list l
    ;; is composed only of atoms, by referring to lat? with l
    ;; replaced by (cdr l)

    ; what is the meaning of the line
    ;    ((null? l) #t)
    ; where
    ;    l is now '((and eggs))
    ;; (null? l) asks if l is the null list. if it is null,
    ;; the value is #t. if it is not null, we ask the next
    ;; question. in this case, l is not null, so move to
    ;; the next question.

    ; what is the next question?
    ;; (atom? (car l))

    ; what is the meaning of the line
    ;    ((atom? (car l)) (lat? (cdr l)))
    ; where
    ;    l is now '((and eggs))
    ;; (atom? (car l)) asks if (car l) is an atom. if it is,
    ;; then the value is (lat? (cdr l)). if it is not, then we
    ;; move to the next question. in this case, (car l) is not
    ;; an atom, so we ask the next question.

    ; what is the next question?
    ;; #t

    ; what is the meaning of the question #t?
    ;; #t asks if #t is true.

    ; is #t true?
    ;; yes, because the question #t is always true!

    ; #t
    ;; #t

    ; why is #t the last question?
    ;; because we do not need to ask any more questions.

    ; why do we not need to ask any more questions?
    ;; because a list can only be empty, or have an
    ;; atom or a list in the first position.

    ; what is the meaning of the line
    ;    (#t #f)
    ;; #t asks if #t is true. if #t is true -- as it always
    ;; is -- then the answer is #f -- false.

    ; what is
    ;    )))
    ;; these are the closing or matching parentheses of
    ;; (cond, (lambda, and (define, which appear at the
    ;; beginning of a function definition. We sometimes
    ;; call these "aggravation parentheses," and they
    ;; are always put at the end.

    ; can you describe how we determined the value #f
    ; for
    ;    (lat? l)
    ; where
    ;    l is '(bacon (and eggs))
    ;; here is one way to say it:
    ;;  "(lat? l) looks at each item in its argument,
    ;;   to see if it is an atom. if it runs out of
    ;;   items before it finds a list, the value of
    ;;   (lat? l) is #t. if it finds a list, as it did
    ;;   in the example '(bacon (and eggs)), the value
    ;;   (lat? l) is #f."

    ; is (or (null? l) (atom? s)) true or false
    ; where
    ;    l is '(), and
    ;    s is '(d e f g)
    ;; #t,
    ;;    because (null? l) is true where l is '()
    (let ((l '())
          (s '(d e f g)))
      (or (null? l) (atom? s)))

    ; is (or (null? l1) (null? l2)) true or false
    ; where
    ;    l1 is '(a b c), and
    ;    l2 is '()
    ;; #t,
    ;;    because (null? l2) is true where l2 is '()
    (let ((l1 '(a b c))
          (l2 '()))
      (or (null? l1) (null? l2)))

    ; is (or (null? l) (null? s)) true or false
    ; where
    ;    l is '(a b c)
    ;    s is '(atom)
    ;; #f,
    ;;    because neither (null? l) is true where l is '(a b c)
    ;;    nor (null? s) is true where s is '(atom)
    (let ((l '(a b c))
          (s '(atom)))
      (or (null? l) (null? s)))

    ; what does (or ...) do?
    ;; (or ...) asks two questions, one at a time. if the first one
    ;; is true it stops and answers true. Otherwise (or ...) asks
    ;; the second question and answers with whatever the second
    ;; question answers.

    ; is it true or false that a is a member of lat
    ; where
    ;    a is 'tea, and
    ;    lat is '(coffee tea or milk)
    ;; true,
    ;;   because one of the atoms of the lat
    ;;     '(coffee tea or milk)
    ;;   is the same as the atom a, namely 'tea

    ; is (member? a lat) true or false, where
    ;   a is 'poached, and
    ;   lat is '(fried eggs and scrambled eggs)
    ;; false,
    ;;   since a is not one of the atoms of lat

    ; this is the function member?
    (define member?
      (lambda (a lat)
        (cond ((null? lat) #f)
              (#t (or
                   (eq? (car lat) a)
                   (member? a (cdr lat)))))))
    ; what is the value of (member? a lat), where
    ;   a is 'meat, and
    ;   lat is '(mashed potatoes and meat gravy)
    ;; #t
    ;;   because the atom 'meat is one of the atoms
    ;; of the lat,
    ;;    '(mashed potatoes and meat gravy)
    (let ((a 'meat)
          (lat '(mashed potatoes and meat gravy)))
      (member? a lat))

    ; how do we determine the value #t for the above application?
    ;; the value is determined by asking the questions about
    ;;     (member? a lat)
    ;; hint: write down the function member? and refer to it while
    ;; you work on the next group of questions.

    ; what is the first question asked by (member? a lat)
    ;; (null? lat)
    ;; this is also the first question asked by lat?

    #|
    The First Commandment

    Always ask null? as the first question in expressing any function.
    |#

    ; what is the meaning of the line
    ;   ((null? lat) #f)
    ; where
    ;   lat is '(mashed potatoes and meat gravy)
    ;; (null? lat) asks if lat is the null list. if it is, then the value
    ;; is #f, since the atom 'meat was not found in lat. if not, then we
    ;; ask the next question. in this case, it is not null, so we ask the
    ;; next question.

    ; what is the next question?
    ;; #t

    ; why is #t the next question?
    ;; because we do not need to ask any more questions

    ; is #t really a question?
    ;; yes, #t is a question whose value is always true

    ; what is the meaning of the line
    ;          (#t (or
    ;               (eq? (car lat) a)
    ;               (member? a (cdr lat))))
    ;; now that we know that lat is not null, we have to
    ;; find out whether the car of lat is the same atom
    ;; as a, or whether a is somewhere in the rest of the
    ;; lat. The question
    ;;   (or
    ;;     (eq? (car lat) a)
    ;;     (member? a (cdr lat)))
    ;; does this

    ; is
    ;   (or
    ;     (eq? (car lat) a)
    ;     (member? a (cdr lat)))
    ; true or false, where
    ;  a is 'meat, and
    ;  lat is '(mashed potatoes and meat gravy)
    ;; we will find out by looking at each question in turn

    ; is (eq? (car lat) a) true or false, where
    ;   a is 'meat, and
    ;   lat is '(mashed potatoes and meat gravy)
    ;; #f,
    ;;    because 'meat is not eq? to 'mashed,
    ;;    the car of
    ;;      '(mashed potatoes and meat gravy)

    ; what is the second question for (or ...)
    ;; (member? a (cdr lat))
    ;;    this refers to the function with the argument lat
    ;;    replaced by (cdr lat)

    ; now what are the arguments for member
    ;; a is 'meat, and lat is now (cdr lat), specifically
    ;;   '(potatoes and meat gravy)

    ; what is the next question?
    ;; (null? lat)
    ;;    remember The First Commandment

    ; is (null? lat) true or false, where
    ;   lat is '(potatoes and meat gravy)
    ;; #f, namely false

    ; what do we do now?
    ;; ask the next question

    ; what is the next question?
    ;; #t

    ; what is #t?
    ;; #t, namely true

    ; what is the meaning of
    ;   (or
    ;     (eq? (car lat) a)
    ;     (member? a (cdr lat)))
    ;; (or (eq? (car lat) a) (member? a (cdr lat)))
    ;; finds out if a is eq? to the car of lat or if
    ;; a is a member of the cdr of lat by referring
    ;; to the function.

    ; is a eq? to the car of lat
    ;; no, because a is 'meat and the car of lat is
    ;; potatoes

    ; so what do we do next?
    ;; we ask (member? a (cdr lat))

    ; now, what are the arguments of member?
    ;; a is 'meat, and
    ;; lat is '(and meat gravy)

    ; what is the next question?
    ;; (null? lat)

    ; what do we do now?
    ;; ask the next question, since (null? lat) is false

    ; what is the next question?
    ;; #t

    ; what is the value of
    ;   (or
    ;     (eq? (car lat) a)
    ;     (member? a (cdr lat)))
    ;; the value of (member? a (cdr lat))

    ; why?
    ;; because (eq? (car lat) a) is false

    ; what do we do now?
    ;; recur -- refer to the function with new arguments

    ; what are the new arguments?
    ;; a is 'meat, and lat is '(meat gravy)

    ; what is the next question?
    ;; (null? lat)

    ; what do we do now?
    ;; since (null? lat) is false, ask the next question

    ; what is the next question?
    ;; #t

    ; what is the value of
    ;   (or
    ;      (eq? (car lat) a)
    ;           (member? a (cdr lat)))
    ;; #t,
    ;;   because (car lat), which is 'meat, and a which is
    ;;   'meat, are the same atom. therefore, (or ...)
    ;;   answers with #t.

    ; what is the value of the application
    ;   (member? a lat)
    ; where
    ;   a is 'meat, and
    ;   lat is '(meat gravy)
    ;; #t,
    ;;   because we have found that 'meat is a member of
    ;;     '(meat gravy)

    ; what is the value of the application
    ;   (member? a lat)
    ; where
    ;   a is 'meat, and
    ;   lat is '(and meat gravy)
    ;; #t,
    ;;   because 'meat is also a member of the lat
    ;;     '(and meat gravy)

    ; what is the value of the application
    ;   (member? a lat)
    ; where
    ;   a is 'meat, and
    ;   lat is '(potatoes and meat gravy)
    ;; #t,
    ;;   because 'meat is also a member of the lat
    ;;     '(potatoes and meat gravy)

    ; what is the value of the application
    ;   (member? a lat)
    ; where
    ;   a is 'meat, and
    ;   lat is '(mashed potatoes and meat gravy)
    ;; #t,
    ;;   because 'meat is also a member of the lat
    ;;     '(mashed potatoes and meat gravy)
    ;; of course, you noticed that this is our original list

    ; just to make sure you have it right, let's quickly run
    ; through it again
    ;  (define member?
    ;    (lambda (a lat)
    ;      (cond ((null? lat) #f)
    ;            (#t (or
    ;                 (eq? (car lat) a)
    ;                 (member? a (cdr lat)))))))
    ; what is the value of (member? a lat)
    ; where
    ;   a is 'meat, and
    ;   lat is '(mashed potatoes and meat gravy)
    ;; #t,
    ;;   hint: write down the function member? and its arguments
    ;;   and refer to them as you go through the next group of
    ;;   questions.

    ; (null? lat)
    ;; no. move to the next line

    ; #t
    ;; yes.

    ; (or (eq? (car lat a))
    ;     (member? a (cdr lat)))
    ;; perhaps.

    ; (eq? (car lat a))
    ;; no. ask the next question.

    ; what next?
    ;; recur with a and (cdr lat), where
    ;;  a is 'meat, and
    ;;  (cdr lat) is (potatoes and meat gravy)

    ; (null? lat)
    ;; no. move to the next line.

    ; #t
    ;; yes, but (eq? (car lat) a) is false.
    ;;   recur with a and (cdr lat), where
    ;;     a is 'meat, and
    ;;     (cdr lat) is '(and meat gravy)

    ; (null? lat)
    ;; no. move to the next line.

    ; #t
    ;; yes, but (eq? (car lat) a) is false.
    ;;   recur with a and (cdr lat), where
    ;;     a is 'meat, and
    ;;     (cdr lat) is '(meat gravy)

    ; (null? lat)
    ;; no. move to the next line.

    ; (eq? (car lat) a)
    ;; yes, the value is #t

    ; (or
    ;   (eq? (car lat) a)
    ;   (member? a (cdr lat)))
    ;; #t

    ; what is the value of (member? a lat), where
    ;   a is 'meat, and
    ;   lat is '(meat gravy)
    ;; #t

    ; what is the value of (member? a lat), where
    ;   a is 'meat, and
    ;   lat is '(and meat gravy)
    ;; #t

    ; what is the value of (member? a lat), where
    ;   a is 'meat, and
    ;   lat is '(potatoes and meat gravy)
    ;; #t

    ; what is the value of (member? a lat), where
    ;   a is 'meat, and
    ;   lat is '(mashed potatoes and meat gravy)
    ;; #t

    ; what is the value of (member? a lat), where
    ;   a is 'liver, and
    ;   lat is '(bagels and lox)
    ;; #f

    ; let's work out why it is #f. what's the first question member? asks?
    ;; (null? lat)

    ; (null? lat)
    ;; no, move to the next line.

    ; #t
    ;; yes, but (eq? (car lat) a) is false.
    ;;   recur with a and (cdr lat), where
    ;;     a is 'liver, and
    ;;     (cdr lat) is '(and lox)

    ; (null? lat)
    ;; no, move to the next line.

    ; #t
    ;; yes, but (eq? (car lat) a) is false.
    ;;   recur with a and (cdr lat), where
    ;;     a is 'liver, and
    ;;     (cdr lat) is '(lox)

    ; (null? lat)
    ;; no, move to the next line.

    ; #t
    ;; yes, but (eq? (car lat) a) is still false.
    ;;   recur with a and (cdr lat), where
    ;;     a is 'liver, and
    ;;     (cdr lat) is '()

    ; (null? lat)
    ;; yes.

    ; what is the value of (member? a lat), where
    ;   a is 'liver, and
    ;   lat is '()
    ;; #f

    ; what is the value of
    ;   (or
    ;     (eq? (car lat) a)
    ;          (member? a (cdr lat)))
    ; where
    ;   a is 'liver, and
    ;   lat is '(lox)
    ;; #f

    ; what is the value of (member? a lat), where
    ;   a is 'liver, and
    ;   lat is '(lox)
    ;; #f

    ; what is the value of
    ;   (or
    ;     (eq? (car lat) a)
    ;          (member? a (cdr lat)))
    ; where
    ;   a is 'liver, and
    ;   lat is '(and lox)
    ;; #f

    ; what is the value of (member? a lat), where
    ;   a is 'liver, and
    ;   lat is '(and lox)
    ;; #f

    ; what is the value of
    ;   (or
    ;     (eq? (car lat) a)
    ;          (member? a (cdr lat)))
    ; where
    ;   a is 'liver, and
    ;   lat is '(bagels and lox)
    ;; #f

    ; what is the value of (member? a lat), where
    ;   a is 'liver, and
    ;   lat is '(bagels and lox)
    ;; #f


    ;;; exercises, chapter 2

    ; for these exercises,
    ;     l1 is '(german chocolate cake)
    ;     l2 is '(poppy seed cake)
    ;     l3 is '((linzer) (torte) ())
    ;     l4 is '((bleu cheese) (and) (red) (wine))
    ;     l5 is '(() ())
    ;     a1 is 'coffee
    ;     a2 is 'seed
    ;     a3 is 'poppy

    ; 2.1
    ;   what is the value of: (lat? l1)
    (let ((l1 '(german chocolate cake)))
      (lat? l1))
    ;; #t

    ;   what is the value of: (lat? l2)
    (let ((l2 '(poppy seed cake)))
      (lat? l2))
    ;; #t

    ;   what is the value of: (lat? l3)
    (let ((l3 '((linzer) (torte) ())))
      (lat? l3))
    ;; #f

    ; 2.2 for each case in exercise 2.1 step through the
    ;     application as we did in this chapter

    (lat? '(german chocolate cake))
    ;; (null? l) -> #f
    ;; (atom? (car l)) -> #t
    ;; recur (lat? '(chocolate cake))
    ;; (null? l) -> f
    ;; (atom? (car l)) -> #t
    ;; recur (lat? '(cake))
    ;; (null? l)
    ;; (atom? (car l)) -> #t
    ;; recur (lat? '())
    ;; (null? l) -> #t
    ;; result -> #t

    (lat? '(poppy seed cake))
    ;; (null? l) -> #f
    ;; (atom? (car l)) -> #t
    ;; recur (lat? '(seed cake))
    ;; (null? l) -> #f
    ;; (atom? (car l)) -> #t
    ;; recur (lat? '(cake))
    ;; (null? l) -> #f
    ;; (atom? (car l)) -> #t
    ;; recur (lat? '())
    ;; (null? l) -> #t
    ;; result -> #t

    (lat? '((linzer) (torte) ()))
    ;; (null? l) -> #f
    ;; (atom? (car l)) -> #f
    ;; #t -> #f
    ;; result -> #f

    ; 2.3 what is the value of (member? a1 l1), and (member? a2 l2) ?
    ; step through the application for each case

    (let ((l1 '(german chocolate cake))
          (a1 'coffee))
      (member? a1 l1))
    ;; (null? lat) -> #f
    ;; (eq? (car lat) a) -> #f
    ;; recur (member? 'coffee '(chocolate cake))
    ;; (null? lat) -> #f
    ;; (eq? (car lat) a) -> #f
    ;; recur (member? 'coffee '(cake))
    ;; (null? lat) -> #f
    ;; (eq? (car lat) a) -> #f
    ;; recur (member? 'coffee '())
    ;; (null? lat) -> #t
    ;; result -> #f

    (let ((l2 '(poppy seed cake))
          (a2 'seed))
      (member? a2 l2))
    ;; (null? lat) -> #f
    ;; (eq? (car lat) a) -> #f
    ;; recur (member? 'seed '(seed cake))
    ;; (null? lat) -> #f
    ;; (eq? (car lat) a) -> #t
    ;; result -> #t

    ; 2.4 rewrite all the functions in this chapter using (if ...) instead of (cond ...)
    (define lat2?
      (lambda (l)
        (if (null? l)
            #t
            (if (atom? (car l))
                (lat2? (cdr l))
                #f))))

    (define member2?
      (lambda (a lat)
        (if (null? lat)
            #f
            (or (eq? (car lat) a)
                (member2? a (cdr lat))))))

    ; 2.5 write the function nonlat? which determines whether a list is the
    ;     empty list or does not contain atomic S-expressions.

    (define nonlat?
      (lambda (l)
        (if (null? l)
            #t
            (if (atom? (car l))
                #f
                (nonlat? (cdr l))))))

    ;; (nonlat? l1) -> #f
    (let ((l1 '(german chocolate cake)))
      (nonlat? l1))

    ;; (nonlat? l2) -> #f
    (let ((l2 '(poppy seed cake)))
      (nonlat? l2))

    ;; (nonlat? l3) -> #f
    (let ((l3 '((linzer) (torte) ())))
      (nonlat? l3))

    ;; (nonlat? l4) -> #t
    (let ((l4 '((bleu cheese) (and) (red) (wine))))
      (nonlat? l4))

    ; 2.6 write a function member-cake? which determines whether a lat contains the atom cake

    (define member-cake?
      (lambda (lat)
        (cond ((null? lat) #f)
              (#t (or
                   (eq? (car lat) 'cake)
                   (member-cake? (cdr lat)))))))

    ;; (member-cake? l1) -> #t
    (let ((l1 '(german chocolate cake)))
      (member-cake? l1))

    ;; (member-cake? l2) -> #t
    (let ((l2 '(poppy seed cake)))
      (member-cake? l2))

    ;; (member-cake? l3) -> #f
    (let ((l3 '((linzer) (torte) ())))
      (member-cake? l3))

    ;; (member-cake? l4) -> #f
    (let ((l4 '((bleu cheese) (and) (red) (wine))))
      (member-cake? l4))

    ; 2.10 the function member? tells whether some atom appears at least once in a lat.
    ;      write a function member-twice? which tells whether some atom appears at least
    ;      twice in a lat.

    ; cheater: we haven't seen filter yet    
    (define member-twice?
      (lambda (a lat)
        (> (length
            (filter
             (lambda (e)
               (eq? e a))
             lat))
           1)))

    ; less of a cheat, although we haven't seen length yet
    (define member-twice?-helper
      (lambda (a lat res)
        (cond ((null? lat) res)
              ((eq? (car lat) a) (member-twice?-helper a (cdr lat) (cons a res)))
              (#t (member-twice?-helper a (cdr lat) res)))))

    (define member-twice?
      (lambda (a lat)
        (> (length (member-twice?-helper a lat '())) 1)))

