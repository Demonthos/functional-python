import dis
import builtins
import inspect
from functools import wraps

#BUILTINS = {name for name, function in sorted(vars(builtins).items()) if inspect.isbuiltin(function) or inspect.isfunction(function)}
BUILTINS = {name for name, function in vars(builtins).items()}

def functional(func):
    global BUILTINS
    
    hasGlobals = False
    
    #print(f'checking{function.__name__}:')
    for i in dis.get_instructions(func):
        if str(i.argval) == str(i.argval).upper() or str(i.argval)[:2] == '__':
            #print('static ', end = '')
            continue
        
        if str(i.argval) in BUILTINS:
            #print('builtin ', end = '')
            continue
        
        either = True
        if i.opname == 'LOAD_GLOBAL': print('global loaded', i)
        elif i.opname == 'STORE_GLOBAL': print('global stored', i)
        else: either = False
        #else: print('ignored:', i)
        if either:
            hasGlobals = True
            break
    if hasGlobals:
        raise SyntaxError(f'{func.__name__} uses globals')
    
    @wraps(func)
    def _wrapper(*args, **kwargs):
        return func(*args, **kwargs)
    
    return _wrapper
