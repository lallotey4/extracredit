  .data
prompt_msg: .asciiz "Enter a positive integer greater than 20:"
error_msg: .asciiz "Illegal number\n"
result_msg: .asciiz "Greatest common divisor:\n"
no_gcd: .asciiz "No common divisor (other than 1)\n"

  .text
  .globl main

main:
#input validation (L,M,N)
  jal input_validation
  move $t0, $v0 #inputting validation for L
  jal input_validation
  move $t1, $v0
  jal input_validation
  
