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
  move $t2, $v0

#to calculate and print the greatest common divisor
  jal calculate_gcd

#exit program
  li $v0, 10
  syscall

#func to validate user the user's input
input_validation:
  li $v0, 4  #syscall: print_str
  la $a0, prompt_msg
  syscall

  li $v0, 5  #syscall: read_int
  syscall

  #check if it qualifies as an illegal input
  bgt $v0, 20, legal_input
  j illegal_input
  
