Introduction to Recursion

    Recursion - when a method calls itself

    When an occurence such as infinite recursive loop happens, this will crash system due to SystemStackError: 
        stack level too deep => when we call a method, some of the system's memory must be allocated to execute 
        that method call, known as adding to the stack. 

    Recursive Method
        - consists of two fundamental parts:
            Base Case - halt the recursion by not making further call
            Recursive Step - continue the recursion by making another subsequent call

            example:

            def count_down(num)
                # base case - stop the recursion
                if num == 0
                    p "Houston, we have lift-off!"
                    return
                end

                p num
                # recursive step - call the same method again
                count_down(num - 1) 
            end

    Recursive Factorial Notes
        factorial problem ex.
        
        def factorial(n)
            return 1 if n == 1
            n * factorial(n - 1);
        end

            factorial(5) # => 120
    
    Solving a Problem Recursively:
    Because every recursive problem must have a base and recursive case, we can follow these steps to help us write a recursive method:

    1.) Identify the base case in the problem and code it. The base case should explicitly handle the scenario(s) where the arguments are so trivially "small", that we immediately know the result without further calculation. Be sure it works by testing it.
    
    2.) Solve the next level of the problem, using the result of the base case. Test it.

    3.) Modify the code in step 2, generalizing it for every level of the problem.

    Recursive Fib Notes
        fibbonacci problem ex.

        def fib(n)
            return 1 if n == 1 || n == 2
            fib(n - 1) + fib(n - 2)
        end


    When is Recursion appropriate?
        - recursion is used to solve problems that can be decompsed into smaller versions of the same problem.

    Spaceship Operator Notes
        <=> - used to compare two values
            - will return -1, 0, or 1. The behavior is as follows, 
                given the expression a <=> b

                it will return -1 if a is less than b
                it will return 0 if a is equal to b
                it will return 1 if a is greater than b

    NIL as Falsey Notes
        - nil & false are the only falsely values
        - everything else is truthy

        || - logical OR
            - under the hood:
                when a is truthy, return a
                when a is falsey, return b

        examples:
        true || 42          # => true
        42 || true          # => 42
        false || 42         # => 42
        42 || false         # => 42
        false || "hello"    # => "hello"
        nil || "hello"      # => "hello"
        "hi" || "hello"     # => "hi"
        0 || true           # => 0
        false || nil        # => nil

    Default Procs
        ||=     pattern is utilized heavily when implementing default procs.
        
        ex: (below, nil was not explicitly assign to prc because prc is automatically nil if method is called without passing in a proc)

        def call_that_proc(val, &prc)
            prc ||= Proc.new { |data| data.upcase + "!!" }
            prc.call(val)
        end

        p call_that_proc("hey")                                             # => "HEY!!"
        p call_that_proc("programmers") { |data| data * 3 }                 # => "programmersprogrammersprogrammers"
        p call_that_proc("code") { |data| "--" + data.capitalize + "--"}    # => "--Code--"

    Lay Initialization
        - deisgn strategy where we delay creation of an object until it is needed.
        - for ex. assigning this within the getter method with ||= and call it in when necessary.