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

legal_input:
  jr $ra

illegal_input:
  li $v0, 4  #syscall: print_str
  la $a0, error_msg
  syscall
  j input_validation

#function to calc GCD
calculate_gcd:
  move $t3, $t0  #t3 = L

gcd_loop:
  move $t4, $t1  #t4 = M
  move $t5, $t2  #t5 = N

inner_gcd_loop:
  beq $t4, $zero, done_gcd  #if t4/M = 0, GCD -> t3/L
  move $t6, $t3  #t6 = t3, L
  div $t5, $t4    #t3 (L) = t5(N)/t4(M)
  mfhi $t3        #t3(L) = remainder of the division

  #swap t4 (M) and t5 (N) for the next iteration
  move $t5, $t4
  move $t4, $t3
