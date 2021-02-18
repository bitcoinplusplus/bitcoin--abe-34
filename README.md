# bitcoin++--abe-34
Fix string index out of range doing catch_up


 if opcode <= opcodes.OP_PUSHDATA4:
      nSize = opcode
      if opcode == opcodes.OP_PUSHDATA1:
        nSize = ord(bytes[i])
        i += 1
        if i + 1 > len(bytes):
          vch = "_INVALID_NULL"
          i = len(bytes)
        else:
          nSize = ord(bytes[i])
          i += 1
      elif opcode == opcodes.OP_PUSHDATA2:
        (nSize,) = struct.unpack_from('<H', bytes, i)
        i += 2
        if i + 2 > len(bytes):
          vch = "_INVALID_NULL"
          i = len(bytes)
        else:
          (nSize,) = struct.unpack_from('<H', bytes, i)
          i += 2
      elif opcode == opcodes.OP_PUSHDATA4:
        (nSize,) = struct.unpack_from('<I', bytes, i)
        i += 4
        if i + 4 > len(bytes):
          vch = "_INVALID_NULL"
          i = len(bytes)
        else:
          (nSize,) = struct.unpack_from('<I', bytes, i)
          i += 4
      if i+nSize > len(bytes):
        vch = "_INVALID_"+bytes[i:]
        i = len(bytes)
