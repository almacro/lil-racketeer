    #lang racket

    ;;; preliminaries

    ; add definitions needed by the text
    ;;(define add1 (let ((f +)) (lambda (x) (f x 1))))
    ;;(define sub1 (let ((f -)) (lambda (x) (f x 1))))
    (define atom? (let ((f1 pair?) (f2 not)) (lambda (x) (f2 (f1 x)))))
