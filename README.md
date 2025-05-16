# task1




      def strict(func):
          def wrapper(*args):
              annotations = func.annotations
              param_names = list(annotations.keys())[:-1] if 'return' in annotations else list(annotations.keys())

              for arg, name in zip(args, param_names):
                  expected_type = annotations[name]
                  if not isinstance(arg, expected_type):
                      raise TypeError(
                          f"Argument '{name}' must be {expected_type.name}, got {type(arg).name}"
                      )

              return func(*args)
         return wrapper


    @strict
    def sum_two(a: int, b: int) -> int:
        return a + b


    print(sum_two(1, 2))    # >>> 3
    print(sum_two(1, 2.4))  # >>> TypeError
