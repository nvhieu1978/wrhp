1
00:00:08,170 --> 00:00:12,640
Before I come to the main topic of
today's lecture, 

2
00:00:12,700 --> 00:00:16,720
I briefly want to talk about an important point that


3
00:00:16,750 --> 00:00:18,340
it was brought up by one of the pioneers after watching the first lecture.

4
00:00:19,480 --> 00:00:24,940
If you recall in the auction example
that I showed you,

5
00:00:24,940 --> 00:00:30,400
 I created three endpoints, "start" to start the
auction, bid to make a bid, 

6
00:00:30,460 --> 00:00:36,580
and then close to finalize the auction to
for close there were two scenarios.

7
00:00:36,970 --> 00:00:44,300
Either there was a bid high enough in
that case when invoking close 

8
00:00:44,320 --> 00:00:48,910
the token  goes to the highest bidder and the highest
bid goes to the seller of the token.

9
00:00:49,630 --> 00:00:53,890
And if there was no such bid,
then on invoking close, 

10
00:00:53,890 --> 00:00:55,120
the token goes back to the seller.

11
00:00:56,715 --> 00:01:01,015
And this pioneer asked the question,
what would happen 

12
00:01:01,035 --> 00:01:07,095
if the close endpoint wasn't there and surely the money couldn't
stay forever be locked in the contract.

13
00:01:07,875 --> 00:01:12,795
And that is a really important point
because what you have to realize is that the blockchain itself,

14
00:01:12,795 --> 00:01:18,525
 the UTxOs on the blockchain are just data, they're absolutely passive.

15
00:01:18,525 --> 00:01:20,715


16
00:01:20,895 --> 00:01:24,855
So in order for anything to happen, there must be a transaction.

17
00:01:25,275 --> 00:01:28,545
So in order to make progress, in order to change the state of the blockchain,

18
00:01:28,545 --> 00:01:33,465
 there must be a new transaction being submitted from somebody

19
00:01:33,495 --> 00:01:39,315
 or from the outside that consumes various UTxOs and produces new ones.

20
00:01:40,110 --> 00:01:45,330
So only new transactions change the state, an UTxO it's just a passive thing, just passively sitting there.

21
00:01:45,330 --> 00:01:47,400


22
00:01:47,820 --> 00:01:50,820
So it will never spring into action by itself and do something.

23
00:01:50,940 --> 00:01:54,870
So you can't have a smart contract that sits on the blockchain.

24
00:01:54,870 --> 00:01:57,990
And then at some point suddenly performs an action.

25
00:01:58,080 --> 00:02:02,760
If you want anything to happen, it must always be triggered by a transaction

26
00:02:02,760 --> 00:02:07,720
and transactions always come from the outside from a user, from a wallet.

27
00:02:08,880 --> 00:02:14,220
Therefore we really need this close endpoint if we want the auction to be settled.

28
00:02:14,490 --> 00:02:15,839


29
00:02:17,109 --> 00:02:24,010
So, of course, in my example, the close was manually  triggered, so I invoke that in the simulator.

30
00:02:24,030 --> 00:02:25,740


31
00:02:26,310 --> 00:02:31,920
Obviously you could write a contract for the wallet that runs on the wallet in a way that automatically does that.

32
00:02:32,250 --> 00:02:34,130


33
00:02:34,359 --> 00:02:39,975
So, when we talk about how to write scripts for the wallet later,

34
00:02:40,275 --> 00:02:43,905
you will see that, that you can do quite sophisticated logic.

35
00:02:44,115 --> 00:02:50,055
So you could do something that automatically sleeps until the deadline is reached in the auction example

36
00:02:50,055 --> 00:02:55,155
that then automatically invokes the close endpoint

37
00:02:55,275 --> 00:02:56,955
and triggers the close transaction.

38
00:02:57,885 --> 00:03:00,255
But, from the point of view of the blockchain, that doesn't matter

39
00:03:00,255 --> 00:03:03,375
it's always an external trigger that does something.

40
00:03:03,495 --> 00:03:06,855
So nothing happens if it's not externally triggered.

41
00:03:07,365 --> 00:03:09,765
So that's a very important to keep in mind.

42
00:03:10,445 --> 00:03:13,055
And thank you very much for bringing that up.

43
00:03:15,595 --> 00:03:20,184
I've explained in the first lecture that they are two parts, two sides

44
00:03:20,204 --> 00:03:24,075
to a smart contract, an on-chain part and an off-chain part.

45
00:03:25,035 --> 00:03:30,585
The on-chain part is about validation, it allows nodes to validate a given transaction and decide

46
00:03:30,585 --> 00:03:33,405
whether the transaction is valid.

47
00:03:33,435 --> 00:03:38,084
And when it, whether it's allowed to consume a given UTxO and

48
00:03:38,084 --> 00:03:43,454
the off-chain part lives in the user's wallet and constructs and

49
00:03:43,454 --> 00:03:45,435
submits suitable transactions.
50
00:03:45,855 --> 00:03:50,475
So both are important topics and we have to master both in order to write smart contracts,

51
00:03:50,475 --> 00:03:55,305
 but for now I want to concentrate on the on-chain part.

52
00:03:56,325 --> 00:04:01,065
So let's recall the extended UTxO model where the idea was that 

53
00:04:01,365 --> 00:04:04,274
we introduce the new type of addresses.

54
00:04:04,885 --> 00:04:10,545
So, the type of addresses used in the simple UTxO model is so-called public key

55
00:04:10,545 --> 00:04:14,655
addresses where the address is given by public key or the hash of a public key.

56
00:04:15,465 --> 00:04:21,795
And if a UTxO sits at such a public key address, then a transaction can consume that UTxO as an input.

57
00:04:21,825 --> 00:04:24,675


58
00:04:24,735 --> 00:04:30,645
If the signature belonging to that public key is included in the transaction.

59
00:04:31,515 --> 00:04:36,825
And what the (E)UTxO model does is extend this by adding a new type of addresses

60
00:04:36,825 --> 00:04:42,615
 so called script addresses that can run arbitrary logic.

61
00:04:43,515 --> 00:04:48,855
And then when a transaction that wants to consume a UTxO sitting at 

62
00:04:48,855 --> 00:04:56,055
a script address is validated by a node, the node will run the script, 

63
00:04:56,055 --> 00:05:00,905
and then depending on the result of the script, decide whether the transaction is valid or not.

64
00:05:02,615 --> 00:05:05,755
And recall that they've two more additions.

65
00:05:05,755 --> 00:05:09,215
So one was that now instead of just having signatures on transactions,

66
00:05:09,215 --> 00:05:13,385
 we have so-called redeemers arbitrary pieces of data.

67
00:05:15,505 --> 00:05:21,775
And on the UTxO side, on the output side, we have an additional arbitrary

68
00:05:21,775 --> 00:05:25,555
piece of data called datum, which you can think of as a little piece of state that sits at the UTxO.

69
00:05:25,555 --> 00:05:27,775


70
00:05:29,065 --> 00:05:34,495
Finally, we have the context and then I explained last time that there are various choices,

71
00:05:34,495 --> 00:05:36,655
 what this context could be.

72
00:05:37,284 --> 00:05:41,215
It could be very restricted, just consisting of the redeemer, or it

73
00:05:41,215 --> 00:05:44,485
could be very global consisting of the whole state of the blockchain.

74
00:05:45,295 --> 00:05:52,465
But as I said in Cardano, it is the transaction that is being validated, including all its inputs and outputs.

75
00:05:52,705 --> 00:05:55,345


76
00:05:56,965 --> 00:06:05,385
So there are three pieces of data that a Plutus script gets, the datum sitting at

77
00:06:05,385 --> 00:06:12,914
the UTxO, the redeemer coming from the input and a validation and the context

78
00:06:12,945 --> 00:06:17,594
consisting of the transaction being validated and it's inputs and outputs.

79
00:06:18,885 --> 00:06:23,865
So in a concrete implementation like Plutus, these three pieces of data

80
00:06:23,955 --> 00:06:29,325
obviously have to be represented by some concrete data type, a Haskell data type.

81
00:06:30,224 --> 00:06:35,985
And as it happens, the choice was made to use the same data type for

82
00:06:35,985 --> 00:06:40,965
all three of them, at least at the low level implementation of Plutus.

83
00:06:41,174 --> 00:06:46,164
So we'll look at that first, but in real life, nobody would actually use

84
00:06:48,090 --> 00:06:52,620
this low level and there are more convenient ways to use more suitable

85
00:06:52,620 --> 00:06:57,420
data types for these things and view we'll come to that a bit later today.

86
00:06:57,870 --> 00:07:02,880
But first I want to talk about this low level implementation of validation.

87
00:07:04,110 --> 00:07:09,539
So datum, redeemer, and context all use the same Haskell data

88
00:07:09,539 --> 00:07:11,250
type and we'll look at that first.

89
00:07:13,140 --> 00:07:19,260
This Haskell data type is defined in the package plutus-core in

90
00:07:19,780 --> 00:07:27,659
plutus-core/src/PlutusCore/Data.hs
and it is called simply data.

91
00:07:29,460 --> 00:07:35,340
And if we look at the definition of this data data type, you see it

92
00:07:35,340 --> 00:07:40,995
has five constructors and isn't run of the mill algebraic data type.

93
00:07:41,085 --> 00:07:45,885
So it has five constructors, Constr it takes an integer andrecursively a list of data.

94
00:07:45,885 --> 00:07:47,745


95
00:07:49,515 --> 00:07:55,065
Then a constructor map that takes a list of pairs of two data items.

96
00:07:55,245 --> 00:08:01,665
So you can think of it as a lookup table with key value pairs where both the

97
00:08:01,665 --> 00:08:07,815
key and the value are data again, then the list constructor that takes a list

98
00:08:07,815 --> 00:08:13,815
of data, the I constructor that takes an integer 

99
00:08:13,815 --> 00:08:16,335
and the B constructor that takes a string or rather a byte string.

100
00:08:17,475 --> 00:08:23,015
And for those of you who are familiar with the JSON format for example, 

101
00:08:24,005 --> 00:08:26,314
this is very similar to something like JSON.

102
00:08:26,685 --> 00:08:32,425
I mean, the constructors are not exactly the same, but like JSON, it can represent numbers and strings and lists of data.

103
00:08:32,445 --> 00:08:37,245


104
00:08:38,669 --> 00:08:39,870
And key value pairs.

105
00:08:40,919 --> 00:08:46,040
So it's what I would call, even though that's probably not an official thing.

106
00:08:46,400 --> 00:08:47,900
I would call a blop type.

107
00:08:48,020 --> 00:08:54,020
So it's, it can basically represent arbitrary data,

108
00:08:54,050 --> 00:08:57,860
Which makes it very suitable for, for our purpose,


109
00:08:57,920 --> 00:09:02,000
because, I explained the extended UTxO model, I was always talking about arbitrary custom data.

110
00:09:03,170 --> 00:09:09,340
We can play with this type in the repl, so I'm in this week's code folder

111
00:09:09,410 --> 00:09:13,139
and I fire up a repl with cabal repl.

112
00:09:14,510 --> 00:09:21,680
Now, in order to get access to the data type I can import Plutus Tx.

113
00:09:23,220 --> 00:09:27,630
It wasn't defined in Plutus Tx, but it gets exported or re-exported from Plutus Tx.

114
00:09:27,630 --> 00:09:29,580


115
00:09:30,090 --> 00:09:35,340
So if I do colon I for info and ask for information about the data type,

116
00:09:35,340 --> 00:09:39,840
Then I basically see the same that we just saw in the source code.

117
00:09:41,819 --> 00:09:45,960
And here we also see where it is actually defined.

118
00:09:47,430 --> 00:09:54,990
Now I can play with this so I can try to define values of this type.

119
00:09:55,020 --> 00:09:58,110
So for example, I can use the I constructor with an integer.

120
00:09:58,140 --> 00:10:05,130
So, The I 42 that can ask for the type, and that is indeed of type data.

121
00:10:06,210 --> 00:10:10,170
If I want to use the B constructor, I need a byte string 

122
00:10:10,170 --> 00:10:18,600
and the easiest way to quickly get a byte string is to
activate an extension at GHT extension

123
00:10:18,600 --> 00:10:20,550
that's called strings.

124
00:10:22,574 --> 00:10:26,964
And what that overloaded strings extension does, normally in Haskell literal strings are of type string,

125
00:10:27,015 --> 00:10:33,615
The Haskell string type, which is just a synonym for lists of characters.

126
00:10:33,615 --> 00:10:35,985


127
00:10:36,704 --> 00:10:41,535
But with this extension I can use literal strings for other string like types as well.

128
00:10:41,535 --> 00:10:43,094


129
00:10:43,094 --> 00:10:46,635
And one of those string like types is the byte string type.

130
00:10:47,055 --> 00:10:51,524
So now that I have this extension, I can now use the constructor,

131
00:10:52,214 --> 00:10:58,055
for example, Haskell, and I get
again something of type data.

132
00:10:58,265 --> 00:11:02,645
And of course I can also use the more complex constructors like mapi.

133
00:11:02,885 --> 00:11:08,105
So if I have the mapi, now I need a list of pairs of data, key value pairs.

134
00:11:08,765 --> 00:11:14,995
So for example, one key could be I 42 and the value could be Haskell.

135
00:11:16,355 --> 00:11:19,770
And the key can also be more complex.

136
00:11:19,800 --> 00:11:22,440
So I can, for example, use the List constructor.

137
00:11:23,430 --> 00:11:34,830
I don't know, Ii 0 and as value Ii 1000 and again, I get something of type data.

138
00:11:38,040 --> 00:11:44,989
In order to write our first validator, I create a new Haskell module, I called it gift and I more 

139
00:11:45,010 --> 00:11:51,390
or less just copy pasted all the language extensions 

140
00:11:51,390 --> 00:11:54,510
and the imports from last week's auction example.

141
00:11:57,360 --> 00:12:04,790
Now let's write the validator and of course the validator itself in the end

142
00:12:04,910 --> 00:12:12,885
will be a script living on the blockchain in Plutus core, low level language based 
143
00:12:12,885 --> 00:12:17,724
on the Lambda calculus, but we don't have to write Plutus core, we'll write Haskell.

144
00:12:17,925 --> 00:12:23,954
And I will explain later how we convert that Haskell into Plutus core script.

145
00:12:25,064 --> 00:12:29,295
So we write a Haskell function that represents our validator.

146
00:12:29,655 --> 00:12:30,964
Let's call it make validator.

147
00:12:31,694 --> 00:12:33,885
So what is the signature of this function?

148
00:12:35,204 --> 00:12:40,555
As we know from the UTxO model, these validation scripts, these validators

149
00:12:40,814 --> 00:12:45,675
get three pieces of information, the datum, the redeemer, and the
150
00:12:45,675 --> 00:12:50,295
context, the datum comes from the output that is being consumed.

151
00:12:50,834 --> 00:12:55,214
The redeemer comes from the input that is consuming, 

152
00:12:55,214 --> 00:12:59,175
and the context is the consuming transaction with all its inputs and outputs.

153
00:12:59,594 --> 00:13:06,315
And as I just said, at this low level, all three types, datum, redeemer 

154
00:13:06,315 --> 00:13:10,455
and context are represented by the data type that we just looked at.

155
00:13:10,995 --> 00:13:15,465
So this will be a function that takes three arguments, all of type data.

156
00:13:17,325 --> 00:13:21,645
And it so happens that the first one is the datum, 

157
00:13:21,645 --> 00:13:24,345
the second one is the redeemer and the third one is the context.

158
00:13:26,415 --> 00:13:28,275
So now what is the return type?

159
00:13:28,665 --> 00:13:32,625
And that is somewhat surprising it's unit.

160
00:13:32,685 --> 00:13:37,605
So this opening closing parentheses it's the unit type in Haskell.

161
00:13:37,605 --> 00:13:43,815
It's a built-in type and it is similar to the void type in mainstream languages like C# or C or Python or Java.

162
00:13:43,935 --> 00:13:47,355


163
00:13:48,765 --> 00:13:53,895
And this type, the unit type only has one value, which is also called unit.

164
00:13:54,525 --> 00:13:59,475
So if we go back to the repl, start up a new repl.

165
00:14:01,125 --> 00:14:04,995
And let's load this module I called gift.

166
00:14:06,435 --> 00:14:11,385
So there's this value, it's also called unit and it looks exactly like the type unit.

167
00:14:11,385 --> 00:14:13,305


168
00:14:14,085 --> 00:14:19,605
And if I ask for the type and it's of type unit, and that is the only value.

169
00:14:19,695 --> 00:14:24,225
So that means this type or value of this type doesn't carry any

170
00:14:24,225 --> 00:14:27,455
information because there's only exactly one value of this type.

171
00:14:30,065 --> 00:14:35,255
Now, if you are somewhat more familiar with Haskell, you will be surprised

172
00:14:35,255 --> 00:14:40,805
about this signature because in Haskell it's very rare that we have a function with a return type of unit.

173
00:14:40,805 --> 00:14:43,345


174
00:14:45,115 --> 00:14:49,695
In other, in mainstream programming languages, you often see functions 

175
00:14:49,695 --> 00:14:52,065
or procedures with the result type of void.

176
00:14:52,935 --> 00:14:56,655
And the value of such functions lies in the side effects.

177
00:14:57,195 --> 00:15:00,925
The end result is not interesting result or in the Haskell

178
00:15:00,945 --> 00:15:04,545
case, a unit result carries no information as I just said.

179
00:15:04,635 --> 00:15:07,725
We know what the result of the function will be, it will be unit.

180
00:15:08,445 --> 00:15:10,944
So why would you bother writing such a function.

181
00:15:11,295 --> 00:15:15,405
Now in other languages, the reason is that in other languages functions can have arbitrary side effects.


182
00:15:15,405 --> 00:15:16,995

183
00:15:17,175 --> 00:15:21,915
So a function with return type unit in Java, 

184
00:15:21,915 --> 00:15:29,355
for example, could write something to the screen or do networking or access the hard drive or whatever.

185
00:15:30,345 --> 00:15:33,585
In Haskell that's not possible, not with the signature.

186
00:15:34,935 --> 00:15:39,735
That would be indicated by an IO to indicate that it has side effects

187
00:15:40,064 --> 00:15:42,675
 I'll get to that a bit in a later lecture.

188
00:15:43,515 --> 00:15:48,015
So this is very unusual and the way it works is there's one thing

189
00:15:48,015 --> 00:15:52,585
that a Haskell function can do
apart from returning a result.

190
00:15:52,585 --> 00:15:55,935
And that is, it can have an error or an exception, it can fail.

191
00:15:56,985 --> 00:16:02,025
So the way validators work at this low level is that if there's no error,

192
00:16:02,085 --> 00:16:07,775
 then validation passes and if there's an error, then it fails.

193
00:16:09,345 --> 00:16:14,915
So in order to write the simply most validator possible, 

194
00:16:15,105 --> 00:16:20,295
we can write a validator that completely ignores all three inputs and always passes.

195
00:16:20,955 --> 00:16:25,305
So we can ignore by using underscores for the inputs that indicates that 

196
00:16:25,305 --> 00:16:30,395
we don't care about the value and we simply return unit.

197
00:16:31,785 --> 00:16:36,885
So this is arguably the simplest validator you can possibly write,

198
00:16:37,485 --> 00:16:39,285
 it completely ignores its three arguments.

199
00:16:39,285 --> 00:16:42,315
It doesn't care about the datum,it doesn't care about the redeemer,
200
00:16:42,315 --> 00:16:46,755
it doesn't care about the context and it immediately returns unit

201
00:16:46,995 --> 00:16:50,485
without having or producing an error.

202
00:16:51,675 --> 00:16:57,895
So that means it always passes, it doesn't care what datum, redeemer, contexts are, it always passes validation.

203
00:16:57,965 --> 00:17:01,125


204
00:17:02,685 --> 00:17:05,775
And what does that mean for the corresponding script address?

205
00:17:05,805 --> 00:17:11,365
So recall, a script address is more or less the hash of the validator.

206
00:17:11,714 --> 00:17:17,415
So I'll show in a second, how we turn this Haskell function into Plutus core script.

207
00:17:17,954 --> 00:17:22,244
And then if you take the hash of that script, you get the

208
00:17:22,244 --> 00:17:23,714
address, this script address.

209
00:17:24,194 --> 00:17:28,454
So what would it mean to have an output sitting at this script address?

210
00:17:28,815 --> 00:17:34,485
Well, would mean that arbitrary transactions can use that output as input.

211
00:17:35,745 --> 00:17:41,025
Arbitrary, because it doesn't matter what redeemer is used, it doesn't matter

212
00:17:41,025 --> 00:17:46,305
what datum was used at the output, and it doesn't matter what structure the transaction that consumes that input has.

213
00:17:46,305 --> 00:17:48,885


214
00:17:50,025 --> 00:17:58,275
So that's why I call this module gift, because if anybody sends funds to this script address, 

215
00:17:58,275 --> 00:18:04,725
then anybody elsecan immediately consume that output and use it for their own purposes.

216
00:18:04,845 --> 00:18:06,765


217
00:18:07,605 --> 00:18:11,145
So if you send ADA to this address, it's a gift.

218
00:18:11,265 --> 00:18:13,515
Anybody can immediately take it.

219
00:18:16,990 --> 00:18:22,419
We should check in the repl, we should reload and let's ignore the warnings.

220
00:18:22,419 --> 00:18:25,870
 they are just unused imports.

221
00:18:26,169 --> 00:18:27,939
So we don't get an error.

222
00:18:29,110 --> 00:18:35,139
We should always frequently switch between the repl and the editor and save our work frequently 

223
00:18:35,590 --> 00:18:39,490
and try to load it into the repl to see that everything is still fine.

224
00:18:40,360 --> 00:18:45,760
It's a nightmare if you write hundreds of lines of code without ever checking

225
00:18:45,760 --> 00:18:50,260
whether compiles and then you get hundreds or thousands of compiler errors.

226
00:18:50,710 --> 00:18:59,230
So ideally your program should always compile, so I made it a habit to very

227
00:18:59,230 --> 00:19:04,319
frequently save my work and checking the repl whether it still compiles.

228
00:19:08,285 --> 00:19:12,695
Now that we have defined this Haskell function, we want an actual validator,

229
00:19:13,615 --> 00:19:15,815
and that is of type validator.

230
00:19:16,845 --> 00:19:23,495
And in order to get the validator, we have to compile this function

231
00:19:23,495 --> 00:19:27,765
to Plutus script and take this script to create a validator.

232
00:19:28,445 --> 00:19:31,565
So let me first write down how we can do this.

233
00:19:33,035 --> 00:19:37,065
And that uses an advance Haskell feature called template Haskell.

234
00:19:38,035 --> 00:19:45,605
And I'll explain it in a minute, but the good news is that the pattern how

235
00:19:45,605 --> 00:19:50,255
 this is used in order to work with Plutus is always the same.

236
00:19:50,825 --> 00:19:54,515
So you don't really have to understand the intricacies of template Haskell in order to use it.

237
00:19:54,515 --> 00:19:56,225


238
00:19:56,255 --> 00:19:59,195
It's more or less always a copy paste of the same pattern.

239
00:20:02,765 --> 00:20:07,860
Okay, let's first look at the types in the repl.

240
00:20:08,010 --> 00:20:12,300
So I start the repl again with cabal repl and load the module with colon

241
00:20:12,300 --> 00:20:25,490
L module name, and now I need to import ledger scripts and Plutus Tx.

242
00:20:28,650 --> 00:20:32,510
Now let's first look at the type of make validator script.

243
00:20:35,630 --> 00:20:40,820
Okay, so it produces a validator, which is what we want, but it takes something

244
00:20:40,820 --> 00:20:46,610
that's of type compiled code parameterized by data to data to data to unit.

245
00:20:47,120 --> 00:20:50,900
So this already looks promising because this is the signature of our make validator function.

246
00:20:50,900 --> 00:20:52,580


247
00:20:55,220 --> 00:21:01,080
So that, I mean, as the name suggests, this type indicates, is the result of compiling a Haskell function of this type.

248
00:21:01,080 --> 00:21:04,380


249
00:21:05,460 --> 00:21:08,790
So let's check what the type of compile is.

250
00:21:10,130 --> 00:21:16,200
That looks a bit scary, but it's mostly because of these qualifications here.

251
00:21:18,710 --> 00:21:26,540
So what this says is it takes an expression of type A 

252
00:21:26,540 --> 00:21:30,680
and compiles it into something of type compiled code of type A.

253
00:21:32,390 --> 00:21:37,280
So in our case, we apply this way is data to data to data to unit.

254
00:21:37,370 --> 00:21:41,270
So we must somehow plug in something of this type, 

255
00:21:41,270 --> 00:21:43,700
the syntax of something of this type.

256
00:21:44,210 --> 00:21:48,260
And we get out the syntax of something of type compiled code A.

257
00:21:49,304 --> 00:21:51,165
So now what's this syntax business.

258
00:21:51,645 --> 00:21:54,465
This is where template Haskell comes in.

259
00:21:55,125 --> 00:22:00,014
So template Haskell does what other programming languages solve with macro systems?

260
00:22:00,044 --> 00:22:01,695


261
00:22:01,754 --> 00:22:03,364
 what's a macro?

262
00:22:03,794 --> 00:22:09,254
Macro is something that gets expanded before the compiler runs.

263
00:22:09,314 --> 00:22:15,885
So it's basically at compile time, macros get somehow evaluated and expended into code,

264
00:22:15,885 --> 00:22:21,824
 that's then inserted next to the code that the user manually typed.

265
00:22:22,335 --> 00:22:25,845
And then the compiler is run over all of that.

266
00:22:25,935 --> 00:22:29,235
So the user code and the expanded macros.

267
00:22:30,225 --> 00:22:36,825
So it's a way to basically generate code at compile time.

268
00:22:37,465 --> 00:22:43,635
So macros are another expression for macros is programs that write programs.

269
00:22:44,205 --> 00:22:46,455
And in Haskell, this is done with template Haskell.

270
00:22:47,105 --> 00:22:54,915
So template Haskell allows you to, to write Haskell functions that produce other Haskell functions

271
00:22:55,185 --> 00:23:00,585
 or Haskell types or general Haskell expressions and insert

272
00:23:00,615 --> 00:23:07,875
those into the source code and then run the compiler over that, to compile

273
00:23:07,875 --> 00:23:10,425
the program and then actually run it.

274
00:23:12,105 --> 00:23:18,435
Right, and so these expressions, this syntax stuff this is

275
00:23:18,435 --> 00:23:21,885
the type of Haskell code.

276
00:23:22,305 --> 00:23:29,235
So something of type expression A, if you have Haskell for example, of type Int,

277
00:23:29,610 --> 00:23:36,360
if you have an Int then exp Int would be
a piece of code that represents an int.

278
00:23:38,750 --> 00:23:45,020
Okay, so if we need a piece of code that represents something of type data to

279
00:23:45,020 --> 00:23:48,379
data to data to unit, I mean, we have our make validator function, but that

280
00:23:48,379 --> 00:23:50,209
is a Haskell function, it's not code.

281
00:23:51,320 --> 00:23:55,070
So somehow having this function, we must get our hands on the

282
00:23:55,210 --> 00:23:58,669
code of that function, the actual syntax, the syntax tree.

283
00:23:59,780 --> 00:24:03,379
And this is what these so-called Oxford brackets are for.

284
00:24:04,429 --> 00:24:10,100
So they allow us to quote the technical term is quote.

285
00:24:10,490 --> 00:24:14,870
So having some Haskell expression, we can quote it using these brackets to get at the underlying syntax tree.

286
00:24:15,260 --> 00:24:18,020


287
00:24:20,620 --> 00:24:22,330
Okay, so this is the first part.

288
00:24:22,330 --> 00:24:25,270
So we have our make validator Haskell function.

289
00:24:25,360 --> 00:24:27,550
We put it in these Oxford brackets.

290
00:24:27,850 --> 00:24:33,610
So the result of that is the syntax tree defining this function.

291
00:24:33,610 --> 00:24:38,230
So you, in principle, you can imagine that the result of this is something like this string that defines the extra function.

292
00:24:38,230 --> 00:24:40,530


293
00:24:40,530 --> 00:24:43,900
It's not really a string, it's a more complicated data type, but you can sort of think of it like that,

294
00:24:43,990 --> 00:24:48,010
 this is now this piece of source code.

295
00:24:48,730 --> 00:24:52,990
Okay, and that is exactly what the compile function expects, and it compiles

296
00:24:52,990 --> 00:24:55,540
 and it produces another syntax tree.

297
00:24:55,570 --> 00:24:58,300
But now Plutus core syntax.

298
00:24:58,750 --> 00:25:06,610
So outcomes, basically the syntactical representation of the compiled make validator function now in the programminglang uage Plutus core,

300
00:25:12,550 --> 00:25:17,370
but this make validator script doesn't expect syntax, it expects an actual script.

301
00:25:18,110 --> 00:25:21,090
And this is now what the double dollar is for.

302
00:25:21,390 --> 00:25:25,680
That is in a way the opposite of the Oxford brackets.

303
00:25:26,100 --> 00:25:31,990
So the Oxford brackets take an expression, a Haskell expression 

304
00:25:32,010 --> 00:25:34,710
and convert it into a syntax tree of that expression.

305
00:25:35,550 --> 00:25:39,300
And the dollar dollar is a so-called splice and it takes a syntax tree 

306
00:25:39,310 --> 00:25:44,460
and splices it into the source code at that point.

307
00:25:45,470 --> 00:25:52,110
So this here gives us basically the Plutus core syntax tree.

308
00:25:52,850 --> 00:25:58,550
And by using this dollar dollar, in the first pass of compilation before the actual compiler runs,
 
309
00:25:58,550 --> 00:26:01,880
 this will run.

310
00:26:01,910 --> 00:26:06,855
So we get the Plutus core syntax and then you can imagine that, 

311
00:26:06,855 --> 00:26:11,294
this point where the dollar is, this syntax will be spliced in.

312
00:26:11,685 --> 00:26:15,794
So that is as if we had hard-coded instead of this, if we had hard-coded

313
00:26:15,794 --> 00:26:20,584
the correct Plutus core expression at this point in the source code.

314
00:26:21,524 --> 00:26:24,764
And then the make validator script function takes this

315
00:26:25,115 --> 00:26:27,875
and turns it into a validator.

316
00:26:29,764 --> 00:26:33,095
But as I said, you don't really have to understand it 

317
00:26:33,095 --> 00:26:34,054
because it's always the same pattern.

318
00:26:34,084 --> 00:26:38,165
We will see somewhat more complicated pattern for so-called parameterized script in a later lecture.

319
00:26:38,165 --> 00:26:39,965


320
00:26:40,865 --> 00:26:44,254
But once you have seen a couple of examples, it always follows the same pattern,

321
00:26:44,254 --> 00:26:48,334
 but still might be good to understand what's going on.

322
00:26:48,875 --> 00:26:53,225
So we have this  Haskell function, it has the logic, use the Oxford brackets

323
00:26:53,225 --> 00:26:56,794
to convert that into a syntactical representation of this function.

324
00:26:57,334 --> 00:27:02,405
And compiler takes its syntactical representation of that Haskell

325
00:27:02,435 --> 00:27:07,810
function, turns it into syntactical representation of corresponding Plutus core function,

326
00:27:07,830 --> 00:27:13,950
 and then the dollar dollar takes that Plutus core 

327
00:27:14,010 --> 00:27:15,780
and splices into the source code at this point.

328
00:27:16,410 --> 00:27:20,580
And then it is as if we had manually type make validator script, 

329
00:27:20,580 --> 00:27:22,830
and then a complicated expression for Plutus core.

330
00:27:23,520 --> 00:27:25,680
And that then turns that into a validator.

331
00:27:27,360 --> 00:27:31,110
Unfortunately, there's one additional thing you have to do.

332
00:27:32,100 --> 00:27:36,690
Normally these Oxford brackets don't allow you to reference definitions outside of them.

333
00:27:36,720 --> 00:27:38,940


334
00:27:39,510 --> 00:27:43,080
So normally you have to inline all your code into these brackets.

335
00:27:43,620 --> 00:27:47,790
So in our case with this extremely simple validator, that wouldn't be a problem.

336
00:27:47,850 --> 00:27:51,060
We could easily not have defined this make validator function.

337
00:27:51,540 --> 00:27:55,110
And just inline here in the brackets wrote this expression.

338
00:27:56,595 --> 00:28:00,705
But of course you can imagine that realistic Plutus validators will be much more complicated

339
00:28:00,705 --> 00:28:05,925
 and you will also want to use helper functions or maybe even library functions

340
00:28:05,925 --> 00:28:10,065
 that are defined elsewhere in order to avoid code duplication.

341
00:28:11,055 --> 00:28:15,555
And you want to maybe reuse pieces of code also in the off-chain part of your contract.

342
00:28:15,555 --> 00:28:17,475


343
00:28:18,375 --> 00:28:21,495
So you don't want to inline everything into these brackets.

344
00:28:21,795 --> 00:28:28,035
You want to have separate definitions of the validator and helper functions.

345
00:28:28,785 --> 00:28:36,075
And normally that wouldn't be allowed, but we can fix this by adding a so-called pragma to our make validator function.

346
00:28:36,105 --> 00:28:38,925


347
00:28:39,495 --> 00:28:41,505
And that's the inlinable pragma.

348
00:28:41,505 --> 00:28:46,125
And as argument it takes the name of the function we want to make inlinable,

349
00:28:46,155 --> 00:28:51,475
 so make validator in our case and this curly brackets minus hash hash minus curly brackets.

350
00:28:51,495 --> 00:28:54,270
351
00:28:54,810 --> 00:28:59,210
This is just a syntax how you do pragmas in Haskell.

352
00:29:01,670 --> 00:29:07,730
So by adding this, we allow the compiler to inline the definition of make validator inside these brackets,

353
00:29:07,730 --> 00:29:11,510
 these Oxford brackets, and then it's fine.

354
00:29:12,469 --> 00:29:16,760
And we would do the same for helper functions that are may be referenced in the make validator function.

355
00:29:16,820 --> 00:29:18,500


356
00:29:19,280 --> 00:29:23,540
So if you look at the source code of Plutus, 

357
00:29:23,540 --> 00:29:27,230
then in certain libraries, especially in the
Plutus prelude, 

358
00:29:27,260 --> 00:29:29,780
you will see this inlinable pragma all over the place.

359
00:29:29,990 --> 00:29:32,929
Virtually every function there has that.

360
00:29:33,709 --> 00:29:37,100
And that is always a good indication that those functions are meant to be used in validators,

361
00:29:37,100 --> 00:29:39,379
 in on-chain code.

362
00:29:39,830 --> 00:29:43,379
Because everything that's supposed to be used in on-chain code needs this pragma.

363
00:29:43,850 --> 00:29:47,860
If you go back to the repl and type validator.

364
00:29:48,510 --> 00:29:53,070
Then it seems to work, but I mean, we don't see much because where  is the Plutus core script,

365
00:29:53,070 --> 00:29:58,620
 it's just indicated with this word script, 

366
00:29:58,650 --> 00:30:02,860
but we can ask for the definition of validator and we see it's just a newtype repl around the script,

367
00:30:02,880 --> 00:30:09,490
 so that we can get access to with get validator.

368
00:30:09,540 --> 00:30:12,610
So let's try this if we have get validator.

369
00:30:14,670 --> 00:30:18,740
Okay, that's also not very enlightening, we just see script, 

370
00:30:18,760 --> 00:30:24,060
but if we ask for information on script, you see,

371
00:30:24,060 --> 00:30:26,010
 we can unwrap that with unscript to get something of type program.

372
00:30:27,210 --> 00:30:28,620
So let's try this.

373
00:30:31,850 --> 00:30:32,990
And we see something.

374
00:30:33,320 --> 00:30:37,430
I mean, it looks very complicated
and those of you who have seen Lambda

375
00:30:37,430 --> 00:30:44,100
calculus before spot that this is some version of the Lambda calculus that

376
00:30:44,100 --> 00:30:48,240
uses De Bruijn index for variables.

377
00:30:48,450 --> 00:30:52,560
But I mean, here you can see the actual honest to god Plutus core script in this representation.

378
00:30:52,560 --> 00:30:54,810


379
00:30:55,380 --> 00:30:58,230
So it worked, we did compile something.

380
00:30:58,980 --> 00:31:03,300
We did compile our make validator function and turned it into Plutus core.

381
00:31:04,260 --> 00:31:10,560
So now we have our first validator, given this validator, we can

382
00:31:10,650 --> 00:31:15,350
create values of two related types that will also be important.

383
00:31:16,260 --> 00:31:18,780
One is validator hash.

384
00:31:19,080 --> 00:31:24,420
So as the name suggests, it's basically just the hash of the validator 

385
00:31:24,420 --> 00:31:29,070
and we can turn our validator into a validator hash by using this validator hash function.

386
00:31:29,790 --> 00:31:35,920
So I call the result valHash and also given the validator,

387
00:31:35,970 --> 00:31:37,500
we can turn it into an address.

388
00:31:38,100 --> 00:31:41,595
So this is a real address on the blockchain.

389
00:31:41,985 --> 00:31:45,255
So we no longer only have pub key addresses.

390
00:31:45,285 --> 00:31:49,575
We also have script addresses and this is how you get it.

391
00:31:49,935 --> 00:31:55,305
So we apply the function script address to the validator and you get an address.

392
00:31:56,385 --> 00:32:04,015
So let me reload and see whether you see anything.

393
00:32:09,175 --> 00:32:14,065
Okay, so the val validator hash indeed looks like a hash.

394
00:32:14,665 --> 00:32:16,615
Yeah, script address.

395
00:32:18,505 --> 00:32:18,775
Okay.

396
00:32:18,775 --> 00:32:23,125
And we see this is more or less just given by this hash.

397
00:32:23,515 --> 00:32:28,135
So the so-called script credential is just this validator hash.

398
00:32:28,995 --> 00:32:32,644
And then there are other informations in a, in an address we see that

399
00:32:32,644 --> 00:32:33,915
is something taken related.
400
00:32:33,915 --> 00:32:38,895
So an address can also always contain staking information 

401
00:32:38,895 --> 00:32:41,324
so that it steaks to a given stake pool.

402
00:32:42,554 --> 00:32:45,945
But we see essentially this script address just consists of the hash of the validator.

403
00:32:46,004 --> 00:32:47,955


404
00:32:49,364 --> 00:32:54,135
And it is important to keep in mind that most of this code is boiler plate.

405
00:32:54,614 --> 00:32:59,145
So the actually business logic, the validation logic in this example is just in this line 

406
00:32:59,324 --> 00:33:05,264
where we say validation always succeeds, no matter what

407
00:33:05,264 --> 00:33:09,965
datum or redeemer or the transaction that spends it are or look like.

408
00:33:11,655 --> 00:33:16,575
Then the rest you will see in this form or very similar in all Plutus code.

409
00:33:17,024 --> 00:33:22,260
So the way to take this Haskell function that gives the business logic of validation 

410
00:33:22,260 --> 00:33:25,810
and turns it into an actual validator by compiling into Plutus core script,

411
00:33:25,830 --> 00:33:30,050
 and then how to take that validator and turn it into a validator hash on address.

412
00:33:30,050 --> 00:33:32,879


413
00:33:34,490 --> 00:33:39,560
So this is just boiler plate, the only interesting line is line 34.

414
00:33:40,760 --> 00:33:44,490
Now, of course, in order to try this, we also need an off-chain part.

415
00:33:45,139 --> 00:33:49,590
And because the focus of this lecture is on validation on on-chain Plutus

416
00:33:49,610 --> 00:33:56,139
and not on off-chain Plutus I've already prepared this, so this is that.

417
00:33:57,135 --> 00:34:01,275
And I don't want to go into any detail, but just briefly go over it.

418
00:34:01,875 --> 00:34:05,865
So this type definition defines the so-called endpoints.

419
00:34:06,655 --> 00:34:11,745
Endpoints are ways for the user to trigger something and enter data,

420
00:34:11,745 --> 00:34:13,815
 give input parameters.

421
00:34:14,235 --> 00:34:16,534
So in this case, I want two endpoints, give and grab.

422
00:34:17,484 --> 00:34:21,375
Give takes an integer parameter, grab doesn't take any parameters, 

423
00:34:21,375 --> 00:34:23,895
which is representative by giving a unit parameter.

424
00:34:24,315 --> 00:34:30,465
So the idea is that somebody can send money, ADA to the script address

425
00:34:30,495 --> 00:34:34,685
we just defined and the integer argument specifies how many lovelace.

426
00:34:35,925 --> 00:34:41,715
And the grab endpoint is for people that want to spend such addresses so that

427
00:34:41,715 --> 00:34:47,415
will just look for all UTxOs sitting at this give address and creating a

428
00:34:47,415 --> 00:34:52,245
transaction that grabs all of those and sends them to the user wallet.

429
00:34:53,324 --> 00:34:58,425
The next I define, the actual behavior of these two, give and grab.

430
00:34:59,595 --> 00:35:05,385
So give taking the integer amount of lovelace, I want to put at that address.

431
00:35:05,925 --> 00:35:09,975
So I create the transaction by specifying constraints.

432
00:35:10,275 --> 00:35:12,315
So this says, must pay to other script.

433
00:35:12,315 --> 00:35:17,355
So this transaction should have an output at a script address, 

434
00:35:17,355 --> 00:35:19,875
which is given by the validator hash.

435
00:35:20,025 --> 00:35:22,545
So this is our script address that we just defined.

436
00:35:22,935 --> 00:35:28,335
And this is one of the points where you need this validator hash with a given datum 

437
00:35:28,335 --> 00:35:33,855
so because of how we define our validator, the datum is completely irrelevant,

438
00:35:33,975 --> 00:35:35,805
 but I must specify one.

439
00:35:35,865 --> 00:35:38,085
So I just picked an arbitrary one.

440
00:35:39,455 --> 00:35:42,645
And then I must specify how much funds.

441
00:35:42,855 --> 00:35:49,225
So ADA dot lovelace value of takes an integer and converts it into lovelace.

442
00:35:50,085 --> 00:35:55,875
So this says the transaction must pay this many lovelace to

443
00:35:56,415 --> 00:35:58,965
that script with this datum.

444
00:36:00,105 --> 00:36:04,395
And this line submits that transaction, this line waits for

445
00:36:04,395 --> 00:36:10,134
confirmation of the transaction and that line logs information.

446
00:36:10,275 --> 00:36:13,725
So in the playground, for example, we can see these log messages,

447
00:36:14,265 --> 00:36:18,654
so that just logs the line made a gift of so-and-so many lovelace.

448
00:36:20,385 --> 00:36:22,785
Now the grab endpoint, no parameters.

449
00:36:23,265 --> 00:36:29,235
This line looks up all UTxOs sitting at this address.
450
00:36:29,235 --> 00:36:33,125
So this is our script address. this will find all UTxOs that sit at that script address.

451
00:36:34,185 --> 00:36:35,714


452
00:36:37,895 --> 00:36:46,609
Then this line gets all their references, references to these UTxOs.

453
00:36:47,569 --> 00:36:53,740
Then I need a so-called lookups in order to tell the wallet basically how to construct the transaction.

454
00:36:53,740 --> 00:36:55,089


455
00:36:55,359 --> 00:36:58,599
So I tell it where to find all those UTxOs.

456
00:36:59,560 --> 00:37:02,649
And I also inform it about the actual validator.

457
00:37:02,830 --> 00:37:09,040
Remember I explained earlier, if you want to consume an UTxO sitting

458
00:37:09,040 --> 00:37:11,980
at the script address, then the spending transaction needs to provide the actual validator code.

459
00:37:11,980 --> 00:37:14,080


460
00:37:14,080 --> 00:37:17,560
Whereas the producing transaction only has to provide the hash.

461
00:37:18,040 --> 00:37:23,569
So this grab is now a spending transaction because I want to grab all the UTXOs.

462
00:37:23,859 --> 00:37:27,910
So I must somehow include the actual validator in that transaction.

463
00:37:28,450 --> 00:37:29,919
This is what that line does.

464
00:37:31,029 --> 00:37:34,600
And then I define the transaction again, giving constraints.

465
00:37:34,600 --> 00:37:40,140
So in this case I have a list of constraints, one for each

466
00:37:40,140 --> 00:37:41,430
UTxO that are found here.

467
00:37:41,490 --> 00:37:45,609
So for each UTxOs sitting at this give address.

468
00:37:45,900 --> 00:37:50,100
I say, okay, the transaction I'm constructing must spend that UTxO

469
00:37:50,759 --> 00:37:52,350
and I must give a reference to it.

470
00:37:52,380 --> 00:37:53,460
I must provide a redeemer.

471
00:37:53,460 --> 00:37:57,660
And again, the redeemer gets ignored by our validator, so I can

472
00:37:57,660 --> 00:37:59,100
do something completely arbitrary.

473
00:37:59,220 --> 00:38:02,790
So I pick this one here and that's it.

474
00:38:02,790 --> 00:38:06,360
So this line basically says, okay, construct a transaction

475
00:38:06,750 --> 00:38:11,999
that spends all those script outputs sitting at this address.

476
00:38:13,110 --> 00:38:19,270
Then there's a variation of the submit Tx
I used in line 78, submit Tx constraints

477
00:38:19,270 --> 00:38:22,935
with that also takes these lookups.

478
00:38:23,085 --> 00:38:28,245
So that allows the compile allow the wallet to construct a transaction that has

479
00:38:28,245 --> 00:38:34,275
a necessary information, how to find those UTxOs and the actually validator script.

480
00:38:34,545 --> 00:38:39,975
Then again, I wait for a confirmation and I log a message collected gifts.

481
00:38:41,055 --> 00:38:46,175
And finally, I put it all together in these endpoints function.

482
00:38:47,855 --> 00:38:54,475
And that basically says, okay the select is  it offers the users choices.

483
00:38:54,815 --> 00:39:03,015
So this means make available, give prime or grab prime, and then afterwards recurs

484
00:39:03,035 --> 00:39:04,535
and do the same over and over again.

485
00:39:05,075 --> 00:39:11,995
And give prime in principle just uses our give that we defined above, 

486
00:39:11,995 --> 00:39:13,835
but, recall the give needs an integer argument.

487
00:39:13,865 --> 00:39:20,910
And this endpoint give, operationally what it does is it will block execution

488
00:39:20,910 --> 00:39:24,270
 and wait for the user to provide an integer.

489
00:39:24,660 --> 00:39:29,860
And once that is provided, execution will continue and will pass on this integer argument to this give function.

490
00:39:29,880 --> 00:39:32,010


491
00:39:32,820 --> 00:39:38,790
And similar for grab, except that grab doesn't expect any arguments so this

492
00:39:38,790 --> 00:39:42,720
will just block until the user unblocks it and then run the grab function.

493
00:39:43,350 --> 00:39:46,620
And because of this select that means at every point in time,

494
00:39:46,650 --> 00:39:47,730
we have these two options.

495
00:39:47,730 --> 00:39:52,920
We can either provide an integer 

496
00:39:52,920 --> 00:39:54,360
and trigger the give or we can not provide anything and trigger the grab.

497
00:39:54,900 --> 00:39:58,680
And after the give or the grab has finished,
498
00:39:58,680 --> 00:40:00,120
 we are again present with the same choices.

499
00:40:01,260 --> 00:40:04,230
So this wraps up all the functionality we want for this example in this one function.

500
00:40:04,230 --> 00:40:05,940

501
00:40:06,600 --> 00:40:10,770
And then there's some boiler plate to generate schema for that in this make no currencies.

502
00:40:10,770 --> 00:40:13,490


503
00:40:13,490 --> 00:40:16,440
So that in the playground we have ADA available.

504
00:40:18,320 --> 00:40:20,420
Let's test this in the playground.

505
00:40:21,050 --> 00:40:26,480
So I started a local playground, as I explained in the first lecture

506
00:40:26,480 --> 00:40:33,240
 and copy pasted the code into the editor and compile it.

507
00:40:45,940 --> 00:40:46,840
And simulate.

508
00:40:49,230 --> 00:40:49,380
Okay.

509
00:40:49,380 --> 00:40:57,030
Let's use three wallets and then give each, I don't know 10 ADA to begin with.

510
00:40:57,270 --> 00:40:59,130
So 10 million lovelace.

511
00:41:05,490 --> 00:41:13,190
And let's say that first, both wallet one,
and wallet two invoke the give endpoint.

512
00:41:14,654 --> 00:41:18,585
So see this give and grab that's exactly the two endpoints


513
00:41:18,585 --> 00:41:20,415
I defined in my off-chain code in the endpoints function.

514
00:41:22,095 --> 00:41:26,654
And the playground picks that up and renders a UI for those.

515
00:41:27,884 --> 00:41:34,845
So I must specify how much, so let's say wallet one gives four ADA = 4 million lovelace, and wallet two 6 ADA.

516
00:41:34,845 --> 00:41:42,815


517
00:41:45,165 --> 00:41:50,055
Okay, then let's wait one block to give those a chance to be incorporated into the simulated blockchain

518
00:41:50,055 --> 00:41:55,544
 and now wallet three grabs.

519
00:41:56,745 --> 00:42:01,544
So grab doesn't take any parameters 

520
00:42:01,575 --> 00:42:06,404
and let's wait again for one block to allow the grab transaction to get onto the blockchain.

521
00:42:08,285 --> 00:42:09,395
Now evaluate.

522
00:42:12,915 --> 00:42:25,540
Ok and we see five transactions, four transactions.

523
00:42:26,320 --> 00:42:29,470
So the first one is as I explained last time, always there that's

524
00:42:29,470 --> 00:42:32,500
the Genesis transaction that distributes the initial funds.

525
00:42:32,560 --> 00:42:33,640
We can see that here.

526
00:42:33,670 --> 00:42:37,330
So that gives 10 ADA to the wallets 1, 2, 3.

527
00:42:38,890 --> 00:42:43,660
Now these two are the give transactions
and they both happen in the same

528
00:42:43,660 --> 00:42:47,950
slot, in slot one, because I
didn't put a wait in between those.

529
00:42:48,940 --> 00:42:51,050
And the grab happens in slot two.

530
00:42:51,250 --> 00:42:53,380
So let's look at the first one.

531
00:42:53,830 --> 00:42:57,700
This happens to be the give of wallet two.

532
00:42:57,730 --> 00:42:59,740
So the other one is the give of wallet one.

533
00:43:00,640 --> 00:43:04,930
So we see the order here doesn't reflect the order in which

534
00:43:04,930 --> 00:43:06,420
we did it in the simulator.

535
00:43:07,320 --> 00:43:09,540
Which makes sense because in the real blockchain is also

536
00:43:09,540 --> 00:43:12,960
indeterministic, it depends on the timing between those two wallets.

537
00:43:14,640 --> 00:43:14,910
Okay.

538
00:43:14,910 --> 00:43:19,620
So wallet two, so the input is the one UTxO that wallet two had, the,

539
00:43:19,650 --> 00:43:24,240
 that comes from the Genesis transaction,
the 10 ADA, and then there are some fees, 

540
00:43:24,240 --> 00:43:30,330
10 lovelace in this case, then this is what goes to the script.

541
00:43:31,080 --> 00:43:31,500
No, sorry.

542
00:43:31,500 --> 00:43:40,380
This is the change, so 4 ADA minus fee go back to the wallet and this is the script.

543
00:43:40,410 --> 00:43:44,120
So this is our shining new script address that we got.

544
00:43:44,580 --> 00:43:50,430
Remember we defined the validator and then hashed it

545
00:43:50,430 --> 00:43:54,810
 and the hash of that at the hash of the validator is more or less the script address.

546
00:43:56,145 --> 00:43:59,955
And we see that now 6 ADA sits at that script address.

547
00:44:00,524 --> 00:44:03,895
If you look at the other give, it's very similar except now it's

548
00:44:03,895 --> 00:44:05,265
wallet one and set of wallet two.

549
00:44:05,265 --> 00:44:09,705
And the amounts are different because here we only gave four ADA to the script.

550
00:44:10,334 --> 00:44:13,064
So six ADA minus fee are changed.

551
00:44:14,475 --> 00:44:19,395
And finally grab, so the off-chain codescan the blockchain for UTxOs sitting at the script address and found those two.

552
00:44:19,395 --> 00:44:21,084


553
00:44:22,214 --> 00:44:27,674
And uses both of them as input and then has to pay some fees,

554
00:44:28,035 --> 00:44:30,694
in this case significantlyhigher than just 10 lovelace.

555
00:44:30,694 --> 00:44:33,314
This is because now scripts are actually executed.

556
00:44:34,095 --> 00:44:39,225
So script execution makes it more expensive the transaction, 

557
00:44:39,225 --> 00:44:43,004
but I don't know whether those costs are realistic yet, probably they are not.

558
00:44:43,634 --> 00:44:46,754
But, we do see that having scripts that need to be validated has an effect on fees.

559
00:44:46,754 --> 00:44:48,345


560
00:44:48,855 --> 00:44:52,455
The amount would probably still change until it's fully calibrated.

561
00:44:54,090 --> 00:44:59,080
And the sum, so the four and the six, ten minus fees go to wallet three.

562
00:44:59,100 --> 00:45:02,880
So wallet three successfully grab those two UTxOs.

563
00:45:03,620 --> 00:45:05,610
Use them as input for this transaction.

564
00:45:06,090 --> 00:45:10,530
And the output is to wallet three's own address.

565
00:45:12,200 --> 00:45:16,380
If we scroll down, let me see how many balances are there in the end.

566
00:45:16,380 --> 00:45:24,270
So we see wallet one ends up with six,  more or less, wallet two with four 

567
00:45:24,270 --> 00:45:30,540
and wallet three with 20, the initial 10 plus the 6 and the 4 that it grabbed from the donations made by the other players.

568
00:45:30,540 --> 00:45:32,460


569
00:45:33,660 --> 00:45:39,880
We also have logs and trace, I can see some more detail about the execution.

570
00:45:41,400 --> 00:45:46,710
So yes, that's the arguably a simplest validator you can write and 

571
00:45:46,710 --> 00:45:51,870
it's of course a bit stupid and silly, but it might even in some situations be useful 

572
00:45:51,870 --> 00:45:57,180
if somebody wants to for whatever reason give ADA away to the community, then in principle, this script address could be used.

573
00:45:57,240 --> 00:45:59,790


574
00:46:02,520 --> 00:46:07,470
For our next example, I just copied the gift module 

575
00:46:07,560 --> 00:46:13,390
that we looked at just now and do a new module and I called that one burn.

576
00:46:13,830 --> 00:46:17,910
But right now the code is identical, so everything is exactly the same.

577
00:46:19,590 --> 00:46:25,530
So the first example, the gift example was a validator that always succeeds.

578
00:46:25,590 --> 00:46:30,390
It ignores its three arguments and always succeeds by returning unit unconditionally.

579
00:46:30,660 --> 00:46:33,090


580
00:46:33,900 --> 00:46:38,610
So in this example, in the burn example, I want to do the opposite.

581
00:46:39,590 --> 00:46:45,705
A validator that again ignores all its three arguments, but then always fails.

582
00:46:46,575 --> 00:46:51,315
So how do we do failure in Plutus, in a Plutus validator,

583
00:46:51,825 --> 00:46:54,285
we have error function for it.

584
00:46:56,805 --> 00:47:02,405
Let me go to the repl and load the burn module.

585
00:47:06,605 --> 00:47:14,225
If I ask for the type of error, I see that it takes a string and returns

586
00:47:14,225 --> 00:47:20,065
an arbitrary type, but this is not the error I am using in the code.

587
00:47:20,255 --> 00:47:23,925
This is the standard Haskell error coming from the Haskell prelude.

588
00:47:24,555 --> 00:47:31,535
So in order to look at the error I'm using, I must import Plutus Tx, 

589
00:47:31,535 --> 00:47:35,355
or I must qualify it with Plutus.Tx.Prelude error.

590
00:47:37,035 --> 00:47:38,625
So this is the one I'm using.

591
00:47:38,625 --> 00:47:41,865
It takes a unit and returns an arbitrary type.

592
00:47:43,335 --> 00:47:45,945
And this brings us to an important point.

593
00:47:47,085 --> 00:47:51,885
I mentioned before when I explained this inlinable pragma that whenever you want

594
00:47:51,885 --> 00:47:56,235
to use, a library function or a helper function inside the validator 

595
00:47:56,625 --> 00:48:01,185
in order for the template Haskell mechanism to work, everything must be inlinable.

596
00:48:01,335 --> 00:48:05,605
So this inlinable pragma has to be edit, but in the standard Haskell

597
00:48:05,625 --> 00:48:09,985
prelude, of course, that's not the case because the standard Haskell prelude

598
00:48:09,985 --> 00:48:14,985
is like decades old and nobody had Plutus in mind when that was written.

599
00:48:15,615 --> 00:48:19,935
So for that reason, the Plutus teamhas provided their own version of a
600
00:48:19,935 --> 00:48:21,855
the Plutus team has provided their own version of a prelude that's suitable for Plutus.

601
00:48:22,665 --> 00:48:32,700
And this is here in, in Plutus.Tx.Prelude, a lot of functions types defined in this standard Haskell prelude,

602
00:48:32,700 --> 00:48:37,390
 have an analog in the Plutus Tx prelude.

603
00:48:38,580 --> 00:48:42,390
The problem is that normally in Haskell by default, 

604
00:48:42,390 --> 00:48:45,960
the standard prelude always gets imported, you
don't have to import it, explicitly

605
00:48:45,960 --> 00:48:47,910
it always gets imported automatically.

606
00:48:48,450 --> 00:48:52,710
And if that was the case here, thenwe would have a lot of name clashes

607 
00:48:52,710 --> 00:48:56,570
between names in the standard prelude and names in the Plutus prelude,

608
00:48:57,090 --> 00:49:01,530
but there is a GHC extension for that, there's no implicit prelude.

609
00:49:01,650 --> 00:49:04,980
So by adding that, the standard Haskell prelude does not get automatically imported.

610
00:49:04,980 --> 00:49:06,420


611
00:49:07,020 --> 00:49:12,000
And by adding this line we import the Plutus prelude instead.

612
00:49:12,630 --> 00:49:16,109
So that's why here when we just say error,

613
00:49:16,210 --> 00:49:21,080
We don't get the standard Haskell error that takes a string, but instead the Plutus error that takes a unit.

614
00:49:22,020 --> 00:49:26,830
If you look down here, I do import something from the standard Haskell prelude as well,

615
00:49:26,850 --> 00:49:30,480
but that's for otherreasons that have nothing to do with validation,

616
00:49:30,510 --> 00:49:34,590
that is for something the off-chain code and for the playground to work, 
617
00:49:34,590 --> 00:49:40,320
for example, the IO I need to import so that the playground doesn't complain.

618
00:49:42,060 --> 00:49:44,510
Another thing is that it can be confusing.

619
00:49:45,560 --> 00:49:49,350
I mean, a lot of the definitions that are in the standard Haskell prelude and in the Plutus prelude,

620
00:49:49,350 --> 00:49:53,750
 we have the same signature and the same behavior, 

621
00:49:53,750 --> 00:49:55,610
but that's not always the case and error is an example.

622
00:49:56,010 --> 00:49:59,120
So the standard one takes a string and the Plutus one does not.

623
00:49:59,570 --> 00:50:03,500
So, one has to be careful, sometimes code that should work,

624
00:50:03,500 --> 00:50:10,030
 I mean, if you have some experience with Haskell and use some ordinary things from the prelude,

625
00:50:10,130 --> 00:50:14,925
then in Plutus suddenly might not work anymore or might work differently.

626
00:50:15,435 --> 00:50:18,045
I also noticed that there are issues with preferences, sometimes operator precedences.

627
00:50:18,045 --> 00:50:20,635


628
00:50:21,215 --> 00:50:26,835
So arithmetic expression or some other combination of operators 

629
00:50:26,865 --> 00:50:30,615
that would work fine without parentheses
in the standard Haskell prelude

630
00:50:30,944 --> 00:50:34,275
suddenly doesn't work in Plutus and you have to add some parentheses.

631
00:50:35,145 --> 00:50:36,495
So we have to be a bit careful there.

632
00:50:37,545 --> 00:50:42,345
Okay, but with this one change, we should now have a validator that always fails.

633
00:50:43,785 --> 00:50:48,195
And if I leave everything as is,I can try this in the playground.

634
00:50:48,885 --> 00:50:53,115
I replaced the code in the editor with this change code where

635
00:50:53,115 --> 00:50:56,925
only the one line has changed replacing unit with error unit.

636
00:50:58,175 --> 00:51:02,375
And my scenario, my simulation is still there.

637
00:51:02,435 --> 00:51:06,035
I think the playground keeps that if the endpoints haven't changed.

638
00:51:06,095 --> 00:51:08,915
And we still have the same endpoints with the same signatures.

639
00:51:09,595 --> 00:51:12,155
So let's evaluate.

640
00:51:16,105 --> 00:51:18,115
Now we see, we only have three transactions.

641
00:51:18,115 --> 00:51:21,175
So the grab obviously failed, which is expected.

642
00:51:21,655 --> 00:51:26,935
The give should still work as before we can send our funds to that new script

643
00:51:26,935 --> 00:51:32,725
address, but it should be impossible to retrieve the funds from there.

644
00:51:33,745 --> 00:51:39,955
And if you scroll down, you see wallet one and wallet two have made the gifts, but

645
00:51:39,995 --> 00:51:42,415
wallet three was not able to grab them.

646
00:51:43,675 --> 00:51:55,145
And if we look at the log we see an error here, wallet error,

647
00:51:55,145 --> 00:52:00,884
validation error, script failure, so we see validation failed.

648
00:52:04,854 --> 00:52:11,380
In the first example, as I said was of a validator, of a script address

649
00:52:11,620 --> 00:52:18,570
that allows arbitrary transactions to consume outputs sitting at that address.
650
00:52:18,900 --> 00:52:22,110
And now we have the opposite where something sitting at that address can never be retrieved.

651
00:52:22,110 --> 00:52:23,940


652
00:52:23,970 --> 00:52:29,700
So it's locked at that UTxO forever, 

653
00:52:29,700 --> 00:52:32,880
no following transaction can ever use those outputs as inputs.

654
00:52:33,330 --> 00:52:40,230
And that's why I called it the module burn, because it's a way to burn your funds,

655
00:52:40,230 --> 00:52:42,540
make them inaccessible forever.

656
00:52:43,230 --> 00:52:47,250
So that also in some circumstances might turn out to be useful.

657
00:52:48,420 --> 00:52:53,880
One thing that's somewhat unsatisfactory is that we don't see why a validation failed.

658
00:52:53,880 --> 00:52:56,565
we just get this evaluation error.

659
00:52:57,315 --> 00:53:01,305
So there's a way around this, a variation on the error function.

660
00:53:01,935 --> 00:53:07,455
So if we check the type of Plutus Tx prelude trace error, 

661
00:53:07,455 --> 00:53:13,755
that takes a Plutus string and produces an error and results in arbitrary type.

662
00:53:14,415 --> 00:53:19,755
So one thing we can do to somewhat improve this is to use trace error instead.

663
00:53:21,915 --> 00:53:26,384
And then it doesn't take unit, it takes a string, so we can use a literal there.

664
00:53:26,775 --> 00:53:29,365
So for example, let's just say "Burnt!".

665
00:53:31,674 --> 00:53:43,115
In order for this to work, we have to use this overloaded strings  extension

666
00:53:43,215 --> 00:53:45,915
that I explained earlier when we wanted to produce a byte string.

667
00:53:46,935 --> 00:53:51,255
As I said, normally string literal only produces a Haskell string.

668
00:53:51,285 --> 00:53:55,095
So if we wanted to also produce a Plutus string, you also need this.

669
00:53:55,125 --> 00:53:55,995
So let's try again.

670
00:53:57,845 --> 00:53:59,295
Okay, now it compiles.

671
00:54:00,395 --> 00:54:05,955
I replaced the code in the editor and evaluated it again.

672
00:54:06,215 --> 00:54:13,425
Here again only get three transactions, but now if you scroll down we see here in

673
00:54:13,425 --> 00:54:19,545
the error message that this log string, the string we defined in the code is now visible here in the playground trace.

674
00:54:19,575 --> 00:54:22,515


675
00:54:23,655 --> 00:54:27,915
So we get some information what went wrong, at least in the playground.

676
00:54:30,254 --> 00:54:35,205
As our next example, let's write a validator that does not completely ignore all its arguments.

677
00:54:35,565 --> 00:54:37,365


678
00:54:37,845 --> 00:54:42,015
So let's say we want a validator that expects a specific redeemer.

679
00:54:43,214 --> 00:54:47,404
So we do here about the redeemer and recall the first argument is the datum, the second is the redeemer

680
00:54:47,404 --> 00:54:50,115
and the third is the context.

681
00:54:50,115 --> 00:54:52,305
So the redeemer is this one.

682
00:54:52,335 --> 00:54:59,595
So let's call it R and let's say validation should pass if the

683
00:54:59,595 --> 00:55:03,194
redeemer is I 42 (Integer 42).

684
00:55:04,125 --> 00:55:11,865
So using this guard so we can say
if it is I 42, then we return unit,

685
00:55:11,875 --> 00:55:18,665
so it passes and otherwise it fails.

686
00:55:25,045 --> 00:55:29,024
Ok, let's see whether it compiles, it does not.

687
00:55:29,024 --> 00:55:29,324
Oh, yeah...

688
00:55:29,324 --> 00:55:34,785
I must, again, I copied the original gift, so I must again have this overloaded strings.

689
00:55:34,785 --> 00:55:36,615


690
00:55:45,755 --> 00:55:46,145
Okay.

691
00:55:47,975 --> 00:55:48,634
So far so good.

692
00:55:49,145 --> 00:55:54,154
Now we should also change the off-chain code in order to try it out, because

693
00:55:54,154 --> 00:55:57,455
I would like to try it out with the correct redeemer and also with the wrong redeemer and see that in the one

694
00:55:57,455 --> 00:56:01,115
case it passes and the other it fails.

695
00:56:01,775 --> 00:56:05,615
And I think the easiest way to do is to also provide an integer argument to the grab endpoint.

696
00:56:05,634 --> 00:56:08,045


697
00:56:09,975 --> 00:56:18,535
So here, let's call that N and then instead of hard coding the

698
00:56:18,535 --> 00:56:21,834
redeemer to I 17, I just use I N.

699
00:56:24,325 --> 00:56:30,390
And then I also have to change this here, 
700
00:56:30,390 --> 00:56:32,259
because now it also has an argument, so I have to pass it onto grab.

701
00:56:34,560 --> 00:56:35,970
Okay, that compiles.

702
00:56:36,629 --> 00:56:41,310
Now, if I go to the playground 
and I replace the code in the editor with our newest version and compile,

703
00:56:41,310 --> 00:56:46,500
and now we see that the scenario

704
00:56:46,589 --> 00:56:48,779
 I prepared for the give and the burn is gone.

705
00:56:49,410 --> 00:56:51,870
And that is because now the endpoints have changed.

706
00:56:51,899 --> 00:56:54,779
Now the grab endpoint suddenly takes an integer parameter.

707
00:56:55,169 --> 00:56:59,640
So in that case, this is gone and I have to redefine the scenario.

708
00:57:00,209 --> 00:57:04,589
I think in this case, it's enough to just use two wallets,

709
00:57:04,589 --> 00:57:07,140
 but let's increase this to 10 ADA each again.

710
00:57:10,220 --> 00:57:14,629
Okay, let's say wallet one gives maybe three ADA.

711
00:57:16,939 --> 00:57:18,250
We wait one block.

712
00:57:20,765 --> 00:57:24,905
Now wallet two grabs and let's first use the wrong redeemer.

713
00:57:25,175 --> 00:57:32,015
So for example, 100 and wait again, and let's try it out.

714
00:57:33,455 --> 00:57:39,665
And we expect grab should fail because
this now uses as redeemer I 42 

715
00:57:39,665 --> 00:57:44,735
and validation will fail in that case,
it should only pass if it's I 42.

716
00:57:45,305 --> 00:57:47,255
Indeed, we only have two transactions.

717
00:57:47,465 --> 00:57:52,135
So this is the Genesis transaction and the give transaction but grab failed.

718
00:57:53,015 --> 00:58:00,095
If we look, so, wallet one gave the three, but wallet two didn't get them.

719
00:58:01,895 --> 00:58:07,785
If we look at the trace, we see validation error, wrong redeemer as expected.

720
00:58:07,885 --> 00:58:17,195
Now, let's go back and change the 100 to 42 and try it again.

721
00:58:20,760 --> 00:58:25,180
And now it seems to have succeeded, we see the third transaction, 

722
00:58:25,200 --> 00:58:29,250
indeed wallet two able to get three ADA minus fees.

723
00:58:30,120 --> 00:58:33,840
We also see this here in the diagram, wallet two now has 13 and the error is gone.

724
00:58:34,110 --> 00:58:37,290


725
00:58:39,000 --> 00:58:43,170
So that's the first example of a validator that actually looks at at least one of its arguments.

726
00:58:43,260 --> 00:58:44,760


727
00:58:46,770 --> 00:58:50,580
So in the next example, I want to show how, instead of using this

728
00:58:50,580 --> 00:58:55,320
low level Plutus, the untyped version we can use a typed version.

729
00:58:55,320 --> 00:59:00,990
So I copied the example that we just looked at into a new module called typed.

730
00:59:02,040 --> 00:59:04,800
And this is just the validator we just saw.

731
00:59:05,760 --> 00:59:11,940
And all these three arguments are of the same type data and that is really very

732
00:59:11,940 --> 00:59:18,040
unpleasant and very unHaskell like it almost feels like programming in a untyped language like JavaScript or Python.

733
00:59:18,060 --> 00:59:19,830


734
00:59:20,790 --> 00:59:23,460
And what we would like is strong types here.

735
00:59:23,669 --> 00:59:31,500
So that only redeemers and datum that actually make sense are expressible.

736
00:59:32,660 --> 00:59:36,620
And it's especially bad with his third argument, the context, because even though it's easy to imagine

737
00:59:36,620 --> 00:59:40,580
 that you can somehow encode a transaction into 

738
00:59:40,580 --> 00:59:46,549
his inputs and outputs into this data type,
it's not at all clear how that is done.

739
00:59:46,700 --> 00:59:50,419
And it would be very complicated to understand that encoding and then use it

740
00:59:50,419 --> 00:59:52,269
in the business logic of the validator.

741
00:59:53,390 --> 00:59:58,939
Luckily we don't have to, and nobody would, instead we would use typed version.

742
00:59:59,720 --> 01:00:03,570
So instead of data, I just pick a type for the datum.

743
01:00:04,400 --> 01:00:07,490
Let's pick the unit type, which makes sense because we completely ignore it in this validator.

744
01:00:07,490 --> 01:00:09,200


745
01:00:09,919 --> 01:00:16,200
And here let's pick integer for the redeemer and instead of datum

746
01:00:16,200 --> 01:00:21,720
there's a type called script context, which is much nicer.

747
01:00:23,040 --> 01:00:28,000
And also I explained earlier that it's very unHaskell like to have a unit

748
01:00:28,020 --> 01:00:32,350
return type and that is also nicer in the typed version of Plutus, that's Bool.

749
01:00:32,730 --> 01:00:37,560
So it's as one would expect, if the result is false validation fails 
750
01:00:37,560 --> 01:00:39,930
the result is true validation succeeds.

751
01:00:41,340 --> 01:00:46,980
Now to convert this into this version, 

752
01:00:47,010 --> 01:00:50,310
the easiest would be to simply say R equals 42.

753
01:00:52,005 --> 01:00:53,215
So if, so, ah...

754
01:00:53,215 --> 01:00:54,745
His Integer is no longer data.

755
01:00:54,765 --> 01:00:56,525
So I can compare it to 42.

756
01:00:56,525 --> 01:01:02,415
And if it is equals 42, the result is true and validation succeeds.

757
01:01:02,445 --> 01:01:05,355
And if it's not 42, then validation fails.

758
01:01:06,315 --> 01:01:09,525
This however would have the same problem that we had before.

759
01:01:09,525 --> 01:01:13,185
When you just used error that in the case of failure, we don't get a nice error message, 

760
01:01:13,185 --> 01:01:19,805
but there's a nice Plutus function call trace if false.

761
01:01:22,235 --> 01:01:23,025
So if...

762
01:01:27,585 --> 01:01:36,785
Plutus Tx prelude trace if false, and we see that takes a string 

763
01:01:36,785 --> 01:01:38,565
and a boolean and returns a boolean.

764
01:01:38,615 --> 01:01:43,095
So the idea is if this boolean is true, 

765
01:01:43,095 --> 01:01:44,385
the result is just true and the string is ignored.

766
01:01:44,805 --> 01:01:48,375
However, if this boolean is false, then the result will be false,

767
01:01:48,675 --> 01:01:50,075
but this string will be log.

768
01:01:50,805 --> 01:01:56,895
And this is exactly what we want here,
so we can use wrong redeemer again as our string

769
01:01:56,895 --> 01:02:01,905
 and then we use this condition.

770
01:02:05,555 --> 01:02:06,404
Oh, okay...

771
01:02:07,315 --> 01:02:08,384
trace if false.

772
01:02:12,055 --> 01:02:15,355
Okay, and that compiles.

773
01:02:16,905 --> 01:02:22,605
Next, we need to adapt our boiler plate,


774
01:02:22,605 --> 01:02:25,095
and this unfortunately in the type version is more complicated and cumbersome.

775
01:02:25,515 --> 01:02:28,935
So let's look at this, first of all, we need something 

776
01:02:28,935 --> 01:02:33,765
that we haven't used before, we introduce a dummy data type equity typed now because of the module name.

777
01:02:33,765 --> 01:02:35,535


778
01:02:36,835 --> 01:02:39,860
And we must provide an instance of a class called validator

779
01:02:39,910 --> 01:02:42,090
types for this dummy data type.

780
01:02:42,630 --> 01:02:46,780
And the purpose of this instance is to somehow wrap together

781
01:02:46,860 --> 01:02:50,700
packing packages together, the datum type and the redeemer type.

782
01:02:50,730 --> 01:02:54,570
So if we give a type instance for the datum type, in our case that's unit,

783
01:02:55,020 --> 01:02:58,680
and we give a type instance for the redeemer type in our case, it's integer.

784
01:02:58,860 --> 01:03:02,700
So this basically just makes a parser out of these two types.

785
01:03:04,140 --> 01:03:08,190
Next we want to compile, and earlier we use this make, make validator script function.

786
01:03:08,190 --> 01:03:09,510


787
01:03:09,840 --> 01:03:14,700
Now we use something called make typed validator, and the result is no longer a validator,

788
01:03:14,730 --> 01:03:19,210
 it's of type typed validator 

789
01:03:19,970 --> 01:03:26,940
and that takes as type parameter this type that we defined here, it's relatively similar.

790
01:03:26,940 --> 01:03:34,350
So first we have to give as a type argument, this type, 

791
01:03:34,350 --> 01:03:36,960
this line is as before more or less.

792
01:03:37,560 --> 01:03:42,540
So we again use Plutus Tx compile, make validator is again with the Oxford

793
01:03:42,540 --> 01:03:49,170
brackets and the dollar dollar, but now we also somehow have to provide a way to interpret

794
01:03:49,230 --> 01:03:54,540
 this typed as untyped as so the boiler plate for this looks like this.

795
01:03:54,540 --> 01:03:58,830
So we have another argument where we again compile a wrap function at 

796
01:03:58,830 --> 01:04:03,570
the wrap function uses a function has provided by the Plutus libraries, that's called wrap validator.

797
01:04:03,570 --> 01:04:05,110


798
01:04:05,580 --> 01:04:09,870
And that also needs two typed arguments, which are again,

799
01:04:09,910 --> 01:04:11,670
 the datum type and the redeemer type.
 800
01:04:12,390 --> 01:04:15,330
So this is also boiler plate and it's always the same, so

801
01:04:15,330 --> 01:04:16,799
you can always copy paste that.

802
01:04:18,600 --> 01:04:24,985
Now in order to get the validator from a typed validator,

803
01:04:24,985 --> 01:04:29,565
 we can use a function called validator script, and it takes a type validator 

804
01:04:29,625 --> 01:04:31,635
and turns it into an untyped validator as we have seen before.

805
01:04:32,685 --> 01:04:36,285
To get the hash, we could, of course use the validator 

806
01:04:36,285 --> 01:04:39,945
we now have, and then turn that into validator hash as we did before.

807
01:04:40,275 --> 01:04:43,035
But there's also more direct way, there's another function called validator hash, 

808
01:04:43,035 --> 01:04:46,875
that's now in a differentmodule, even though it has the same name, 

809
01:04:46,875 --> 01:04:50,685
it's in the typed version of the script and Ledger.Typed.Scripts.

810
01:04:51,575 --> 01:04:58,775
And it takes the typed validator and produces the validator hash.

811
01:04:59,495 --> 01:05:03,905
And finally, the address that's as before, so we take the validator 

812
01:05:03,905 --> 01:05:06,245
and apply the script address function to it.

813
01:05:07,565 --> 01:05:12,525
So, admittedly, this example doesn't really demonstrates nicely 

814
01:05:12,765 --> 01:05:17,415
why we would bother with type validation instead of
untyped as we had before, 

815
01:05:17,505 --> 01:05:22,065
because the boiler plate is much more complicated and
we don't really see an obvious advantage.

816
01:05:22,935 --> 01:05:27,825
I mean, we save two lines of code,
but it barely seems worth it.

817
01:05:28,335 --> 01:05:32,115
But of course, if you have more realistic, more complex examples, 

818
01:05:32,115 --> 01:05:36,705
then it becomes more and more helpful if
you can use specific types 

819
01:05:36,705 --> 01:05:42,475
that are suited to your business case of the validation logic 

820
01:05:42,835 --> 01:05:45,305
and don't have to bother with this block typed data.

821
01:05:46,244 --> 01:05:49,545
And then it becomes much more useful.

822
01:05:50,085 --> 01:05:54,225
So in practice all validation scripts or other scripts in Plutus

823
01:05:54,225 --> 01:05:58,545
will use this typed version, the untyped version will never be used.

824
01:05:59,295 --> 01:06:02,955
Finally, let's look at the off-chain code, 

825
01:06:02,955 --> 01:06:04,904
that is almost identical to what we had before.

826
01:06:05,355 --> 01:06:09,884
There's one slight change here in this line, earlier we had must pay

827
01:06:09,884 --> 01:06:15,555
to other script, but now that we use typed validator,

828
01:06:15,555 --> 01:06:18,525
 there are special convenience functions for the common case that one script  is especially important in off-chain code.

829
01:06:18,525 --> 01:06:21,765


830
01:06:21,765 --> 01:06:26,505
I mean, sometimes you deal with more than one, 

831
01:06:26,505 --> 01:06:31,735
but often the on-chain code is about one specific script 

832
01:06:31,735 --> 01:06:33,735
and then there's this function must pay to these script instead of two other script.

833
01:06:34,245 --> 01:06:40,500
And that has the advantage that you don't have to provide the datum as data,

834
01:06:40,500 --> 01:06:46,440
 but you can provide the datum with the type that you used in the typed validator.

835
01:06:46,440 --> 01:06:49,110
So in our case unit, 
so I can just use unit here.

836
01:06:50,040 --> 01:06:54,000
Apart from that, I believe everything
else is the same as before.

837
01:06:55,890 --> 01:06:59,110
And if we check in the
repl, it also compiles.

838
01:07:00,390 --> 01:07:06,120
Now we could try that in the
playground, but I think it's not interesting

839
01:07:06,120 --> 01:07:10,530
 because the behavior of this code will be exactly as before.

840
01:07:10,920 --> 01:07:17,160
So if we provide 42, then the grab will succeed, and if we provide

841
01:07:17,190 --> 01:07:20,715
a different value, then it will fail, So in the playground, 

842
01:07:20,715 --> 01:07:22,395
you won't be able to see a difference.

843
01:07:22,695 --> 01:07:24,285
We have exactly as before.

844
01:07:25,035 --> 01:07:28,215
Next, let's try to understand how this actually works.

845
01:07:28,635 --> 01:07:33,825
So the typed validators are just this thin layer on top of the untyped ones

846
01:07:34,395 --> 01:07:39,615
and this wrap function, or rather the wrap validator function converts

847
01:07:39,675 --> 01:07:45,855
a function of this type of a typed validator into an untyped version.

848
01:07:46,245 --> 01:07:50,535
And in order to do that, it's obvious that somehow you need to convert

849
01:07:50,535 --> 01:07:54,225
the datum and the redeemer type in our case unit and integer into
850
01:07:54,255 --> 01:07:56,565
data and script context as well.

851
01:07:57,555 --> 01:08:06,345
So this wrap basically what it does is, 
it takes the data arguments that it gets in

852
01:08:06,345 --> 01:08:08,925
the typed version, converts them into...

853
01:08:09,255 --> 01:08:12,674
in this case unit integer and script context, then runs the typed make validator function.

854
01:08:13,065 --> 01:08:14,895


855
01:08:15,795 --> 01:08:19,335
And then if there's an exception, it will return...

856
01:08:19,555 --> 01:08:20,215
No, no...

857
01:08:20,234 --> 01:08:22,934
If there's false it will throw an exception 

858
01:08:22,934 --> 01:08:25,045
and if the result is true it will return true...

859
01:08:26,425 --> 01:08:26,845
unit.

860
01:08:28,854 --> 01:08:33,365
So we need a way or there must be a way to convert between at least unit and integer in data.

861
01:08:33,365 --> 01:08:35,644


862
01:08:36,635 --> 01:08:40,205
And this is done by a class called is data.

863
01:08:41,675 --> 01:08:44,805
This is in module PlutusTx.IsData.Class.

864
01:08:45,965 --> 01:08:49,385
And this class has two functions, to data and from data.

865
01:08:49,385 --> 01:08:54,435
So to data, so if a type A is an instance of this class, 

866
01:08:54,435 --> 01:08:57,875
then to data of an A will convert this into a data.

867
01:08:58,595 --> 01:09:03,095
And from data given a data will try to convert it back into an A, and this can fail,

868
01:09:03,095 --> 01:09:04,755
 so we have this maybe type here.

869
01:09:04,755 --> 01:09:08,854
So if it succeeds, we get just the A and if it fails, we get nothing.

870
01:09:09,965 --> 01:09:16,065
You can try this in the repl, so let's import Plutus Tx

871
01:09:17,175 --> 01:09:20,745
and Plutus Tx is data class.

872
01:09:22,455 --> 01:09:25,335
So we can look for is data here as well.

873
01:09:25,335 --> 01:09:30,255
And we see more or less the same that we saw in the documentation.

874
01:09:32,205 --> 01:09:37,545
And in particular, we see that there are some predefined instances, 

875
01:09:37,545 --> 01:09:47,895
for example, int and bool and integer, and
unit should also be somewhere, here.

876
01:09:49,095 --> 01:09:52,385
So this explains why it worked out of the box for integer

877
01:09:52,385 --> 01:09:54,135
and unit as in our example.

878
01:09:55,455 --> 01:09:58,485
Now let's play with this tom data and from data a bit.

879
01:09:58,485 --> 01:10:02,795
So for example, we can try to data of 42, the integer.

880
01:10:04,620 --> 01:10:09,600
Just make sure it's an integer and
we get I 42, which is not surprising,

881
01:10:09,600 --> 01:10:11,250
that's what we did by hand before.

882
01:10:11,310 --> 01:10:13,560
So when we work with integers in...

883
01:10:14,070 --> 01:10:18,340
as a data value, use the Ii constructor, should also work.

884
01:10:18,390 --> 01:10:23,910
The other way around, so if I do from data I 42, now I must have the compile

885
01:10:23,910 --> 01:10:25,890
 and tell it what type I expect.

886
01:10:25,890 --> 01:10:30,600
So I expect the maybe integer, then it succeeds, so I get a Just and 42.

887
01:10:31,800 --> 01:10:35,580
In order to see it fail, let's take another constructor, for example, 

888
01:10:35,580 --> 01:10:41,100
the list constructor with an empty list and that fails.

889
01:10:41,160 --> 01:10:44,400
So this doesn't correspond to an integer, so if we get nothing.

890
01:10:46,830 --> 01:10:52,755
And we see here that there are some predefined types that have instances.

891
01:10:53,625 --> 01:10:58,905
And that's, as I said, the reason why
it worked in our example, but of course

892
01:10:58,905 --> 01:11:03,465
this is still not completely satisfactory because what we really want is we want to

893
01:11:03,465 --> 01:11:10,425
use custom data types that are very sweet suited for the validator we want to write.

894
01:11:11,295 --> 01:11:14,925
And in order for that to work, normally we would have to write by

895
01:11:14,925 --> 01:11:22,785
hand instances for the is data class for these custom types, which is quite tedious and also quite mechanical.

896
01:11:22,785 --> 01:11:24,555


897
01:11:24,555 --> 01:11:26,475
So we don't really want to do that.

898
01:11:27,195 --> 01:11:30,915
But the good news is we don't have to, because Plutus also provides an

899
01:11:31,065 --> 01:11:36,865
automatic mechanism to use custom types and make them instances of is data.

900
01:11:39,435 --> 01:11:44,535
So finally, let's look at how to make custom data types work with is data and typed validators.

901
01:11:44,625 --> 01:11:46,785


902
01:11:47,655 --> 01:11:54,195
So I copied the typed module underthe name is data, 

903
01:11:54,195 --> 01:12:00,315
and let's say instead of integer for redeemer,
we want a custom data type.

904
01:12:00,375 --> 01:12:13,345
Let's use a simple newtype, my silly
redeemer that just wraps an integer.

905
01:12:14,915 --> 01:12:19,805
And let's try to replace the integer here
where we have the redeemer with this type.

906
01:12:22,655 --> 01:12:27,095
So in order to pattern match, 
we can just pattern match against this.

907
01:12:27,155 --> 01:12:28,595
So R is now an integer again.

908
01:12:28,605 --> 01:12:30,575
So this should still be correct.

909
01:12:31,385 --> 01:12:34,325
Here in the type instances. we have to replace the integer with my silly redeemer.

910
01:12:34,325 --> 01:12:36,275


911
01:12:40,610 --> 01:12:44,059
Okay, this should be fine here, my silly redeemer.

912
01:12:47,389 --> 01:12:50,849
So that should be it for the off-chain code, the on-chain code.

913
01:12:51,559 --> 01:12:55,200
Now for the off-chain code, we must just in the grab instance where 

914
01:12:55,630 --> 01:13:03,320
we give the redeemer, we must somehow now provide the right thing there.

915
01:13:03,320 --> 01:13:05,719
And actually we don't really know what to write there.

916
01:13:06,559 --> 01:13:13,599
So what we can do is to data of my silly redeemer R.

917
01:13:15,610 --> 01:13:18,919
So if we now try to load that module.

918
01:13:23,730 --> 01:13:25,950
We do get, okay.

919
01:13:25,980 --> 01:13:32,329
First we get the error that that is ambiguous.

920
01:13:33,179 --> 01:13:35,030
Let's call it Plutus Tx to data.

921
01:13:39,330 --> 01:13:39,930
Okay.

922
01:13:43,820 --> 01:13:44,240
Okay.

923
01:13:44,300 --> 01:13:51,560
But now we get the error message that no
instance of is data for this class, my silly redeemer, 

924
01:13:51,560 --> 01:13:57,590
 in order to fix that, we could write an instance for is data of my silly redeemer by hand,

925
01:13:57,590 --> 01:14:01,010
 which in this case would prevent if he is straightforward,

926
01:14:01,040 --> 01:14:05,270
because we could somehow reuse the one for integer, but we don't have to.

927
01:14:06,020 --> 01:14:15,740
Instead we can use Plutus Tx unstable make is data, which is again,

928
01:14:15,740 --> 01:14:20,810
 a function using template Haskell like this, let's first see whether that works.

929
01:14:24,345 --> 01:14:24,705
Yes.

930
01:14:24,765 --> 01:14:25,665
Now it compiles.

931
01:14:26,835 --> 01:14:31,005
So this is a template Haskell function,
and it takes a type and the syntax to

932
01:14:31,005 --> 01:14:36,615
provide a type is to use two single quotes in front of the name of the type.

933
01:14:37,725 --> 01:14:43,545
And this will then at compile time, write an instance for is data for this type

934
01:14:43,605 --> 01:14:46,035
and splice it in here at this point.

935
01:14:46,395 --> 01:14:50,685
So this is as if we manually at this position here in the source code had written an instance for is data.

936
01:14:51,075 --> 01:14:53,265


937
01:14:54,535 --> 01:14:57,465
Now actually, we should be able to try that out as well.

938
01:14:57,465 --> 01:15:04,215
So if we, again, import Plutus Tx and Plutus Tx is data class,

939
01:15:05,355 --> 01:15:11,745
and now we do something like to data, my silly redeemer 42.

940
01:15:14,820 --> 01:15:20,310
Then it works and we see it doesn't just what we might have expected, reuse the instance for integer.

941
01:15:20,730 --> 01:15:22,440


942
01:15:22,590 --> 01:15:26,060
So in that case, it would just be I 42, but it uses the constructor of the data class.

943
01:15:26,990 --> 01:15:28,520


944
01:15:30,590 --> 01:15:35,670
So that's not obvious maybe, but that's how it, how it's done.

945
01:15:37,590 --> 01:15:37,860
Okay.

946
01:15:37,860 --> 01:15:41,100
So, and this of course works for other custom types as well.

947
01:15:41,700 --> 01:15:47,820
So using this Plutus as the template Haskell function unstable make is data,

948
01:15:47,820 --> 01:15:55,980
 we can turn custom data types into instances of is data 

949
01:15:55,980 --> 01:15:59,790
and then use them in our validator scripts and now are typed validators.
950
01:16:00,510 --> 01:16:04,470
In case you're wondering why it's called unstable, 
there's also a stable version, which you should use in production code.

951
01:16:04,950 --> 01:16:07,350


952
01:16:08,130 --> 01:16:12,720
So this is about constructors,
we saw that in this case, the my

953
01:16:12,720 --> 01:16:16,600
silly redeemer constructor was translated into constructr zero.

954
01:16:17,490 --> 01:16:21,120
I suppose if there's only one constructor for a data type, it will always be zero.

955
01:16:21,570 --> 01:16:26,240
But if there are several constructors,
it's not so clear in how they are ordered.

956
01:16:26,790 --> 01:16:30,150
And the difference between the unstable and the stable version is

957
01:16:30,150 --> 01:16:34,680
that the unstable version does not make any guarantees that betweendifferent Plutus versions,

958
01:16:34,769 --> 01:16:39,630
 the constructor number corresponding to a given constructor will be preserved.

959
01:16:39,630 --> 01:16:41,490


960
01:16:42,330 --> 01:16:45,690
And that of course would be bad because
if you use an older version of Plutus

961
01:16:45,720 --> 01:16:53,070
to serialize something to data, and then a new version of Plutus makes it in a different way,

962
01:16:53,070 --> 01:16:58,650
 that's it in a different way then it would be incompatible

963
01:16:58,800 --> 01:17:02,565
and you would have version problems
and if you use the stable version,

964
01:17:02,565 --> 01:17:07,095
then you can explicitly specify which constructor corresponds to which index.

965
01:17:07,125 --> 01:17:10,905
So then it's guaranteed to work between
different versions of Plutus, 

966
01:17:10,905 --> 01:17:15,645
but for now for quick and dirty trying, I always use the unstable make is data.

967
01:17:16,215 --> 01:17:19,155
So let's quickly try this out in the playground whether it

968
01:17:19,155 --> 01:17:22,485
still works as before it should be exactly the same behavior.

969
01:17:23,745 --> 01:17:30,175
So I pasted the new code into the editor and compiled and same scenarios

970
01:17:30,195 --> 01:17:32,625
before first with the wrong redeemer.

971
01:17:34,245 --> 01:17:39,255
And here we now get two transactions
and wallet two didn't successfully

972
01:17:39,255 --> 01:17:45,525
grab, now let's provide the right redeemer and try again.

973
01:17:47,145 --> 01:17:50,985
Now we have three transactions,
so the grab worked and the balances are also correct.

974
01:17:50,985 --> 01:17:52,575


975
01:17:53,415 --> 01:17:57,855
So we see that both, the untyped
and the typed version behave

976
01:17:57,855 --> 01:18:03,315
exactly the same, but the typed
version is much nicer to work with.

977
01:18:04,275 --> 01:18:09,195
So to summarize in this lecture have looked at simple examples of validators first untyped and typed.

978
01:18:09,224 --> 01:18:12,825


979
01:18:13,724 --> 01:18:17,535
And we started with a validator that always succeeds, completely ignoring its arguments.

980
01:18:17,535 --> 01:18:18,915


981
01:18:19,634 --> 01:18:24,764
Then a validator that always fails again, completely ignoring its arguments.

982
01:18:25,695 --> 01:18:30,045
Then at one, that actually looks at the redeemer and checks whether.

983
01:18:30,045 --> 01:18:31,995
it has a certain predefined value.

984
01:18:32,715 --> 01:18:38,144
Then we turn that into a typed version,
which is the one that will be used in practice,

985
01:18:38,144 --> 01:18:42,495
 first with built-in data types.

986
01:18:43,184 --> 01:18:48,434
Then we saw how we can also use custom data types, 

987
01:18:48,434 --> 01:18:54,134
but we haven't looked at examples where the datum
or the context is actually inspected.

988
01:18:54,885 --> 01:18:59,295
Which of course in realistic examples will mostly be the case.

989
01:18:59,955 --> 01:19:02,374
So we will do that in next lectures.

990
01:19:05,105 --> 01:19:07,905
Finally, let's look at
some homework for you.

991
01:19:07,995 --> 01:19:10,855
I prepared two models, homework one and homework two.

992
01:19:12,025 --> 01:19:18,514
So in homework one, I changed the redeemer type to a pair of booleans.

993
01:19:19,665 --> 01:19:23,955
And as it says, in the comment, the logic should be that validation should

994
01:19:23,955 --> 01:19:29,594
succeed if these two booleans are the same, true true or false false, and it

995
01:19:29,594 --> 01:19:31,495
should fail if they are not the same.

996
01:19:33,255 --> 01:19:39,315
And so everything should compile,
but I left lots of undefineds here.

997
01:19:39,644 --> 01:19:44,445
And here the logic is wrong, so where 
it says fix me, you have to do something.

998
01:19:45,375 --> 01:19:49,335
And the off-chain code which is not focus of this lecture,

999
01:19:49,335 --> 01:19:51,045
 I already implemented correctly.
 1000
01:19:54,434 --> 01:20:00,065
So, if you look at the playground for this homework one, then here in the grab.

1001
01:20:00,345 --> 01:20:01,875
So this case false, true.

1002
01:20:01,875 --> 01:20:08,385
If I evaluate the grab should fail,
but if I have true true or false the grab should succeed.

1003
01:20:08,385 --> 01:20:10,545


1004
01:20:10,905 --> 01:20:15,995
Finally, the second homework is very similar instead of a pair of booleans, 

1005
01:20:15,995 --> 01:20:21,855
I'm now using a custom data type, my redeemer is a record type with two fields called flag one 

1006
01:20:21,855 --> 01:20:23,934
and flag two both have type bool.

1007
01:20:24,554 --> 01:20:26,345
But the logic again should be the same.

1008
01:20:26,945 --> 01:20:30,645
Validation should succeed, if these two booleans these two, flag one and flag

1009
01:20:30,645 --> 01:20:33,705
two are the same and fail otherwise.

1010
01:20:35,025 --> 01:20:38,415
So in the playground, this looks very similar, 

1011
01:20:38,415 --> 01:20:40,095
except now the UI is rendered a bit differently.

1012
01:20:40,455 --> 01:20:45,224
So the field names appear here,
but same behavior so this should,

1013
01:20:45,285 --> 01:20:50,415
the grab should succeed should also
succeed if both are true, 

1014
01:20:50,415 --> 01:20:54,135
but if one is false and the other is true or
the other way around, it should fail.


