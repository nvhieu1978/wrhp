1
00:00:06,740 --> 00:00:09,320
Welcome to the Plutus Pioneer Program.

2
00:00:09,470 --> 00:00:11,960
We are very excited to have you all here.

3
00:00:13,395 --> 00:00:15,885
So, let me first talk about the schedule.

4
00:00:15,885 --> 00:00:20,855
So the idea is that there will
be lectures on every Thursday and

5
00:00:20,955 --> 00:00:23,174
Q & A sessions on every Tuesday.

6
00:00:23,505 --> 00:00:28,455
And in some weeks we might have
additional lectures, for example, guest

7
00:00:28,455 --> 00:00:33,165
lectures or some topics that are not
so relevant for the main curriculum.

8
00:00:34,035 --> 00:00:39,135
And because there are so many of you,
it's unfortunately not possible to

9
00:00:39,585 --> 00:00:42,435
be as interactive as I like it to be.

10
00:00:42,975 --> 00:00:48,335
So it would be great if all of you could
use the discord server to help each other,

11
00:00:48,895 --> 00:00:51,915
answer questions and solve problems.

12
00:00:52,125 --> 00:00:54,875
I mean, we will do what we
can, my colleagues and myself

13
00:00:55,305 --> 00:00:57,745
to answer questions and help.

14
00:00:57,745 --> 00:01:00,915
But with the sheer number of
participants, it's just not possible

15
00:01:00,915 --> 00:01:05,114
to pay as much attention to every
individual as we would like.

16
00:01:05,474 --> 00:01:07,744
So thank you for helping out.

17
00:01:10,485 --> 00:01:15,054
As for the content, so the idea is to
really give a thorough introduction to

18
00:01:15,054 --> 00:01:22,605
Plutus, explain the underlying concepts,
look at various types of contracts.

19
00:01:22,605 --> 00:01:28,675
Look at how we can test contracts in
the playground or also offline, locally.

20
00:01:30,845 --> 00:01:35,475
Talk about native tokens, how
to control minting and burning

21
00:01:35,475 --> 00:01:37,405
of naked tokens in Plutus.

22
00:01:38,205 --> 00:01:42,645
And we also look at how to deploy
a Plutus contract and write a

23
00:01:42,645 --> 00:01:44,535
back-end for Plutus contract.

24
00:01:46,705 --> 00:01:49,590
Plutus learning is not easy unfortunately.

25
00:01:49,759 --> 00:01:56,009
So, you have to be aware that the
cost probably won't be easy and there

26
00:01:56,009 --> 00:01:57,960
are a variety of reasons for that.

27
00:01:58,649 --> 00:02:04,140
So one is that Plutus uses
the so-called UTxO model.

28
00:02:04,410 --> 00:02:10,288
I'll explain in much more detail what
that means later in this lecture, and that

29
00:02:10,288 --> 00:02:17,790
is different and less intuitive than the
Ethereum method for doing smart contracts.

30
00:02:18,150 --> 00:02:24,630
It has a lot of advantages the UTxO
model, but it also requires a new way

31
00:02:24,630 --> 00:02:26,459
of thinking about smart contracts.

32
00:02:26,700 --> 00:02:30,630
So that's one thing, and that's before
we even start with the language itself.

33
00:02:32,400 --> 00:02:36,720
Then of course Plutus has brand new
and still under rapid development.

34
00:02:36,900 --> 00:02:42,720
So probably during the time of the
course there will be significant changes.

35
00:02:42,870 --> 00:02:46,500
So we often have to update
the dependencies on the

36
00:02:46,770 --> 00:02:48,420
main Plutus repository.

37
00:02:48,810 --> 00:02:52,830
And it might be that contracts that
compile at the beginning of the course

38
00:02:52,860 --> 00:02:57,570
won't compile any longer at the end of
towards the end of the course, because

39
00:02:57,960 --> 00:03:00,150
there have been some syntax changes.

40
00:03:01,680 --> 00:03:05,250
In addition to that
tooling is not ideal yet.

41
00:03:05,950 --> 00:03:13,980
So those of you who have experienced
with Haskell and know about the

42
00:03:13,980 --> 00:03:18,840
Haskell tooling, we noticed that in
the presence of Plutus, some of the

43
00:03:18,840 --> 00:03:24,170
tooling is not as pleasant as you
maybe use to being from doing Haskell.

44
00:03:25,620 --> 00:03:31,829
So, sometimes it's a bit painful,
so it's not as easy to get access

45
00:03:31,829 --> 00:03:37,799
to a syntax of functions or to
documentation from the repl, for example.

46
00:03:38,700 --> 00:03:43,049
And it's not even very easy to
build Plutus in the first place.

47
00:03:43,170 --> 00:03:45,690
So your best bet is probably using nix.

48
00:03:46,200 --> 00:03:51,579
You can also try cabal and Stack or
Docker, actually the Plutus team will

49
00:03:51,600 --> 00:03:55,530
provide a nice Docker image at some point.

50
00:03:55,649 --> 00:04:00,260
So maybe that will then be the
easiest option, but yeah, it's

51
00:04:00,260 --> 00:04:05,010
not totally trivial to get Plutus
to compile in the first place.

52
00:04:07,170 --> 00:04:12,060
Then, of course, Plutus
is Haskell more or less.

53
00:04:12,570 --> 00:04:17,880
So on top of the other problems, you
first have to have a firm grip on

54
00:04:18,418 --> 00:04:26,530
a Haskell in order to do Plutus and
obviously in the eight weeks, of course

55
00:04:26,550 --> 00:04:31,370
time, I won't have time to first do
a proper thorough Haskell course.

56
00:04:32,230 --> 00:04:36,470
The Haskell course that I did in
Greece on Barbados in Ethiopia.

57
00:04:36,470 --> 00:04:42,110
And then last year, virtually in
Mongolia were full-time courses, 10

58
00:04:42,110 --> 00:04:44,660
week full-time courses, 40 hours a week.

59
00:04:45,530 --> 00:04:49,670
And even in those courses, we didn't
cover everything that you will

60
00:04:49,670 --> 00:04:54,620
need to fully understand Plutus,
of course we also covered things

61
00:04:54,710 --> 00:04:56,100
that are irrelevant for Plutus.

62
00:04:56,120 --> 00:04:59,840
So it's not as bad as it sounds,
but nevertheless, there is a

63
00:05:00,260 --> 00:05:01,480
quite some Haskell that you need.

64
00:05:02,060 --> 00:05:04,970
And I won't have time to
thoroughly explain everything.

65
00:05:05,010 --> 00:05:09,230
I'll try to explain the special
concepts that you need for Plutus

66
00:05:09,260 --> 00:05:14,360
obviously, and whenever there is a
especially need, when I see that a lot

67
00:05:14,360 --> 00:05:17,940
of you are struggling with something,
then obviously I'll take the time to

68
00:05:19,450 --> 00:05:21,800
explain that topic in more detail.

69
00:05:22,560 --> 00:05:26,539
So, unfortunately I won't be able to
spend as much time teaching Haskell

70
00:05:26,539 --> 00:05:33,330
as I'd like to, because obviously I
mostly want to do Plutus, but we did

71
00:05:33,330 --> 00:05:36,840
recoat our Mongolia Haskell course.

72
00:05:37,229 --> 00:05:41,969
And we have started editing the videos
and making them nicer and more concise.

73
00:05:42,750 --> 00:05:50,320
And what we have, we'll publish here for
you on the discord server, so that, if

74
00:05:50,320 --> 00:05:55,110
you are struggling with Haskell and would
like an introduction, that's much slower,

75
00:05:55,260 --> 00:06:02,510
much slower pace, then you can give those
videos a try, and maybe they help with

76
00:06:02,510 --> 00:06:04,239
the Haskell problems you might have.

77
00:06:05,270 --> 00:06:09,705
Another problem is that Plutus is
brand new, which of course is also

78
00:06:09,705 --> 00:06:15,044
very exciting, but it also means that
you and I and the Plutus team are

79
00:06:15,044 --> 00:06:20,954
the first people ever in the history
of humanity that write Plutus code.

80
00:06:21,195 --> 00:06:25,995
So if you learn another programming
language and you get stuck or have a

81
00:06:25,995 --> 00:06:30,674
problem, then normally you can just go
to stack overflow or Google, and often

82
00:06:30,734 --> 00:06:32,354
you will be lucky and find an answer.

83
00:06:32,775 --> 00:06:36,885
So, because we are the first
you won't have that option.

84
00:06:37,724 --> 00:06:40,455
So we have to figure it
out while we go along.

85
00:06:44,534 --> 00:06:48,615
One of the most important things
you need to understand in order to

86
00:06:48,725 --> 00:06:54,345
write Plutus smart contracts is the
counting model that Cardano uses.

87
00:06:54,765 --> 00:07:01,335
And that is the so-called (E)UTxO model,
which is an abbreviation for extended

88
00:07:01,425 --> 00:07:04,245
unspent transaction output model.

89
00:07:05,355 --> 00:07:09,795
The UTxO model without being
extended is the one that has

90
00:07:09,795 --> 00:07:11,295
been introduced by Bitcoin.

91
00:07:11,895 --> 00:07:13,275
But there are other models.

92
00:07:13,405 --> 00:07:17,535
Ethereum, for example, uses a
so-called account-based model, which

93
00:07:17,535 --> 00:07:24,015
is what you're used do from a normal
bank, where everybody has an account

94
00:07:24,015 --> 00:07:25,875
and each account has a balance.

95
00:07:26,385 --> 00:07:31,215
And if you transfer money from one
account to another, then the balances

96
00:07:31,245 --> 00:07:36,675
get updated accordingly, but that
does not how the UTxO model works.

97
00:07:40,425 --> 00:07:44,375
Unspent transaction outputs
are exactly what the name says.

98
00:07:44,645 --> 00:07:49,955
They are transaction outputs that is
outputs from previous transactions

99
00:07:49,955 --> 00:07:53,285
that happened on the blockchain
that have not yet been spent.

100
00:07:53,495 --> 00:07:59,855
So let's look at an example where we
have two such UTxOs, one belonging

101
00:07:59,855 --> 00:08:05,975
to Alice, 100 ADA and another
one belonging to Bob, 50 ADA.

102
00:08:06,455 --> 00:08:10,455
And as an example, let's assume that
Alice wants to send 10 ADA to Bob.

103
00:08:11,405 --> 00:08:16,055
So she creates a transaction and the
transaction is something that has inputs

104
00:08:16,085 --> 00:08:21,365
and outputs, can be an arbitrary number of
inputs and an arbitrary number of outputs.

105
00:08:22,625 --> 00:08:31,225
And an important thing is that you can
always only use complete UTxOs as input.

106
00:08:31,680 --> 00:08:36,270
So, if she wants to send 10 ADA
to Bob, she can't simply split her

107
00:08:36,270 --> 00:08:40,140
existing 100 ADA into a 90 to 10 piece.

108
00:08:40,140 --> 00:08:43,950
She has to use the full 100 ADA as input.

109
00:08:44,220 --> 00:08:49,530
So by using the UTxO 100 ADA
as input to a transaction.

110
00:08:49,930 --> 00:08:55,730
Alice has no spent that UTxO,
so it's no longer an UTxO.

111
00:08:55,730 --> 00:08:57,990
It's no longer unspent it's been spent.

112
00:09:00,390 --> 00:09:05,295
And now she can create
outputs for a transaction.

113
00:09:05,444 --> 00:09:07,745
So she wants to pay 10 ADA to Bob.

114
00:09:07,905 --> 00:09:12,824
So one output will be 10 ADA to Bob,
and then she wants her change back.

115
00:09:12,824 --> 00:09:16,275
So she creates a second
output of 90 ADA to herself.

116
00:09:17,474 --> 00:09:22,985
And so this is how, even though
you always have to consume complete

117
00:09:22,985 --> 00:09:26,834
UTxOs, you can get your change back.

118
00:09:26,895 --> 00:09:32,594
So you consume the complete UTxO,
but then you create an output for the

119
00:09:32,594 --> 00:09:38,354
change and note that in a transaction,
the sum of the input values must

120
00:09:38,474 --> 00:09:40,275
equal the sum of the output values.

121
00:09:40,275 --> 00:09:45,194
So in this case, 100 ADA go
in and 10 plus 90 ADA go out.

122
00:09:45,974 --> 00:09:48,015
This is strictly speaking, not true.

123
00:09:48,194 --> 00:09:51,694
There are two exceptions, the first
exception is transaction fees.

124
00:09:51,905 --> 00:09:56,925
So in the real blockchain for each
transaction, you have to pay fees.

125
00:09:57,464 --> 00:10:02,715
So that means that the, some of
input values have to, has to be

126
00:10:02,715 --> 00:10:07,035
slightly higher than the sum of output
values to accommodate for the fees.

127
00:10:07,665 --> 00:10:11,775
And the second exception is the
native tokens that we have on Cardano.

128
00:10:12,165 --> 00:10:15,675
So it's possible for transactions
to create new tokens.

129
00:10:15,675 --> 00:10:19,455
In which case the outputs will be
higher than the inputs or to burn

130
00:10:19,455 --> 00:10:23,325
tokens, in which case the inputs
will be higher than the outputs.

131
00:10:23,865 --> 00:10:27,795
But that is a somewhat advanced
topic, how to handle minting and

132
00:10:27,795 --> 00:10:29,515
burning of native tokens in Plutus.

133
00:10:29,835 --> 00:10:31,845
And we'll come back to
that later in the course.

134
00:10:32,595 --> 00:10:36,195
So for now we only look at transactions
where there's some of the input values

135
00:10:36,195 --> 00:10:38,555
equals the sum of the output values.

136
00:10:39,420 --> 00:10:43,589
So this is a first example of a
simple transaction, and we see

137
00:10:43,589 --> 00:10:47,610
that the effect of a transaction
is to consume and spend transaction

138
00:10:47,610 --> 00:10:49,949
output and to produce new ones.

139
00:10:50,339 --> 00:10:56,819
So in this example, one UTxO has been
consumed, Alice original 100 ADA UTxO,

140
00:10:57,240 --> 00:10:59,069
and two new ones have been created.

141
00:10:59,459 --> 00:11:05,939
One 90 ADA UTxO belong to Alice and
another 10 ADA UTxO belonging to Bob.

142
00:11:06,510 --> 00:11:09,689
It's important to note that
this is the only thing that

143
00:11:09,839 --> 00:11:12,989
happens on an UTxO blockchain.

144
00:11:13,589 --> 00:11:17,280
The only thing that happens when
a new transaction is added to the

145
00:11:17,280 --> 00:11:24,089
blockchain is that some form a UTxOs
becomes spent and UTxOs appear.

146
00:11:24,630 --> 00:11:32,150
So in particular, nothing is ever changed,
no value or any other data associated with

147
00:11:32,160 --> 00:11:34,079
the transaction output is ever changed.

148
00:11:34,290 --> 00:11:38,069
The only thing that changes by a
new transaction is that some of the

149
00:11:38,130 --> 00:11:44,189
formerly unspent transaction outputs
disappear and others are created, but

150
00:11:45,150 --> 00:11:47,190
the outputs themselves never change.

151
00:11:47,400 --> 00:11:50,580
The only thing that changes is
whether they are unspent or not.

152
00:11:51,480 --> 00:11:55,950
Let's do one other example, a
slightly more complicated one

153
00:11:56,610 --> 00:12:02,580
where Alice and Bob together want
to pay 55 ADA each to Charlie.

154
00:12:03,480 --> 00:12:06,120
So they create a transaction together.

155
00:12:07,110 --> 00:12:13,170
And as inputs, Alice has no choice, she
only has one UTxO, so she uses that one.

156
00:12:13,590 --> 00:12:18,630
And Bob also doesn't have a choice
because neither of his two UTxOs

157
00:12:19,050 --> 00:12:21,510
is a large enough to cover 55 ADA.

158
00:12:21,690 --> 00:12:25,710
So Bob has to use both his UTxO as input.

159
00:12:29,790 --> 00:12:37,875
This time we need three outputs, one the
55 plus 55 equals 110 ADA for Charlie,

160
00:12:38,595 --> 00:12:43,305
and then two change outputs, one for
Alice's change and one for Bob's change.

161
00:12:43,845 --> 00:12:49,665
So Alice paid 90, so she should
get 35 change and Bob paid 60.

162
00:12:49,725 --> 00:12:51,525
So he should get five change.

163
00:12:54,585 --> 00:12:58,185
One thing, I haven't yet explained
is under which conditions a

164
00:12:58,185 --> 00:13:01,515
transaction can spend a given UTxO.

165
00:13:02,145 --> 00:13:05,715
Obviously it wouldn't be a good
idea if any transaction could

166
00:13:05,715 --> 00:13:10,275
spend arbitrary UTxOs, if that
was the case, then Bob could spend

167
00:13:10,275 --> 00:13:12,645
Alice's money without her consent.

168
00:13:13,995 --> 00:13:19,285
So the way it works is by adding
signatures to transactions, so for

169
00:13:19,305 --> 00:13:24,665
our first example, our transaction
one, because that consumes an

170
00:13:24,665 --> 00:13:26,925
UTxO belong to Allice as input.

171
00:13:28,135 --> 00:13:31,334
Alice's signature has to be
added to the transaction.

172
00:13:31,964 --> 00:13:35,864
And in the second example, because there
are inputs belonging to both Alice and

173
00:13:35,864 --> 00:13:40,875
Bob, both Alice and Bob have to sign
that transaction, which incidentally

174
00:13:40,875 --> 00:13:43,485
is something you can't do in Daedalus.

175
00:13:43,995 --> 00:13:49,905
So you would have to use the Cardano
CLI for complex transactions like that.

176
00:13:51,165 --> 00:13:56,025
Everything I've explained so far
is just about the UTxO model,

177
00:13:56,175 --> 00:13:58,755
not the extended UTxO model.

178
00:13:59,334 --> 00:14:02,655
So this is all just a simple UTxO model.

179
00:14:03,795 --> 00:14:08,385
And the extended part comes in
when we talk about smart contracts.

180
00:14:09,285 --> 00:14:13,994
So in order to understand that,
let's just concentrate on one

181
00:14:14,515 --> 00:14:18,365
consumption offer a UTxO buy an input.

182
00:14:18,974 --> 00:14:25,545
And as I just explained, the validation
that decides whether the transaction.

183
00:14:26,280 --> 00:14:31,830
This input belongs to is allowed to
consume that you take so in the simple

184
00:14:31,830 --> 00:14:35,610
UTxO model relies on digital signatures.

185
00:14:35,670 --> 00:14:39,300
So in this case, Alice has to
sign the transaction for this

186
00:14:39,300 --> 00:14:41,520
consumption of the UTxO to be valid.

187
00:14:42,840 --> 00:14:48,270
And now the idea of the extended UTxO
model is to make this more general.

188
00:14:48,689 --> 00:14:53,460
So instead of just having one condition,
namely that the appropriate signatures

189
00:14:53,870 --> 00:14:55,439
is present in the transaction.

190
00:14:56,010 --> 00:15:01,860
We replace this by arbitrary logic,
and this is where Plutus comes in.

191
00:15:02,700 --> 00:15:07,680
So instead of just having an address
that corresponds to a public key, and

192
00:15:07,680 --> 00:15:13,350
that can be verified by a signature
that is added to the transaction,

193
00:15:13,950 --> 00:15:19,410
instead we have more general addresses
that are not based on public keys or

194
00:15:19,410 --> 00:15:24,660
the hashes of public keys, but instead
contain arbitrary logic that can decide

195
00:15:24,689 --> 00:15:29,760
under which condition this specific
UTxO can be spent by a transaction.

196
00:15:30,540 --> 00:15:33,900
So instead of an address going
to a public key, like Alice's

197
00:15:33,900 --> 00:15:38,529
public key in this example, there
will be an arbitrary script, a

198
00:15:38,529 --> 00:15:40,680
script containing arbitrary logic.

199
00:15:41,250 --> 00:15:48,719
And instead of the signature in the
transaction, the input will justify

200
00:15:48,719 --> 00:15:53,369
that it is allowed to consume this
output with some arbitrary piece

201
00:15:53,369 --> 00:15:55,890
of data that we call the redeemer.

202
00:15:56,969 --> 00:16:04,339
So we replace the public key address,
Alice in our example by a script, and we

203
00:16:04,339 --> 00:16:10,760
replace a digital signature by a redeemer
which is an arbitrary piece of data.

204
00:16:12,060 --> 00:16:14,985
Now, the next question is,
what exactly does that mean?

205
00:16:15,015 --> 00:16:17,025
What do we mean by arbitrary logic?

206
00:16:17,235 --> 00:16:20,564
And in particular it's important
to consider what information?

207
00:16:20,564 --> 00:16:22,605
What context this script has?

208
00:16:23,535 --> 00:16:25,035
So there are several options.

209
00:16:25,395 --> 00:16:32,295
And the one indicated in this diagram is
that all the script sees is the redeemer.

210
00:16:32,355 --> 00:16:36,885
So all the information the script has
in order to decide whether it's okay

211
00:16:36,885 --> 00:16:42,105
for the transaction to consume this
UTxO or not is looking at the redeemer.

212
00:16:42,825 --> 00:16:48,525
And that is the thing that
Bitcoin incidentally does.

213
00:16:48,725 --> 00:16:53,954
So, in Bitcoin, there are smart
contracts, they are just not very smart.

214
00:16:54,015 --> 00:16:58,724
They are called Bitcoin script and
Bitcoin script works exactly like this.

215
00:16:59,265 --> 00:17:04,635
So there's a script on the UTxO site
and to redeemer on the input side and

216
00:17:04,635 --> 00:17:10,034
the script gets the redeemer and can
use the redeemer to decide whether

217
00:17:10,034 --> 00:17:12,905
it's okay to consume the UTxO or not.

218
00:17:13,554 --> 00:17:16,905
But that's not the only option,
we can decide to give more

219
00:17:16,905 --> 00:17:18,254
information to the script.

220
00:17:19,185 --> 00:17:23,385
So, Ethereum uses a different concept.

221
00:17:23,743 --> 00:17:27,674
In Ethereum the script basically can
see everything, the whole blockchain,

222
00:17:27,675 --> 00:17:29,175
the whole state of the blockchain.

223
00:17:30,465 --> 00:17:33,315
So that's like the opposite
extreme of Bitcoin.

224
00:17:33,405 --> 00:17:37,095
Bitcoin the script has very little
context, all it can see is the

225
00:17:37,095 --> 00:17:44,455
redeemer in Ethereum the script, the
solidity scripts in Ethereum can see

226
00:17:44,654 --> 00:17:46,965
the complete state of the blockchain.

227
00:17:48,389 --> 00:17:53,520
So that enables Ethereum's scripts to
be much more powerful so they can do

228
00:17:53,550 --> 00:17:59,370
basically everything, but it also comes
with problems because the scripts are

229
00:17:59,370 --> 00:18:03,370
so powerful, it's also very difficult
to predict what a given script will do

230
00:18:03,479 --> 00:18:08,669
and that opens the door to all sorts
of security issues and dangerous,

231
00:18:08,820 --> 00:18:13,080
because it's very hard to predict for
the developers of an Ethereum smart

232
00:18:13,080 --> 00:18:18,810
contract what can possibly happen
because there are so many possibilities.

233
00:18:20,530 --> 00:18:25,729
So what Cardano does is something
in the middle, so it doesn't

234
00:18:25,729 --> 00:18:29,989
offer such a restricted view as
Bitcoin, but also not such a, not

235
00:18:29,989 --> 00:18:34,340
such a global view as Etherebut,
but instead chooses a middle way.

236
00:18:35,149 --> 00:18:40,399
So the script can see the whole
blockchain, can see the state of the word

237
00:18:40,399 --> 00:18:45,060
blockchain, but it can't see the whole
transaction that is being validated.

238
00:18:45,720 --> 00:18:50,595
So, in contrast to Bitcoin it can just
see this one input, the redeem of this

239
00:18:50,595 --> 00:18:55,605
one input, but it can see that and all
the other inputs of the transaction and

240
00:18:55,605 --> 00:19:00,445
also all the outputs of the transaction
and the transaction itself, and the Plutus

241
00:19:00,465 --> 00:19:06,735
script can use that information to decide
whether it's okay to consume this output.

242
00:19:07,514 --> 00:19:11,595
Now, in this example, there's only
one input, but if this transaction had

243
00:19:11,655 --> 00:19:15,675
more than one input, then the script
would be able to see those as well.

244
00:19:17,264 --> 00:19:23,730
There's one last ingredient that Plutus
scripts need in order to be as powerful

245
00:19:23,730 --> 00:19:25,860
as expressive as Ethereum scripts.

246
00:19:26,430 --> 00:19:33,150
And that is a so-called datum which is
a piece of data that can be associated

247
00:19:33,150 --> 00:19:35,700
with a UTxO an addition to the value.

248
00:19:36,300 --> 00:19:41,700
So at a script address, like in this
example, in addition to this 100 ADA

249
00:19:41,760 --> 00:19:47,430
value, that can be an arbitrary piece
of data attached, which we call datum.

250
00:19:49,090 --> 00:19:55,100
And with this, we can actually
mathematically prove that Plutus is

251
00:19:55,640 --> 00:19:59,960
at least as powerful as Ethereum, so
everything, every logic you can express

252
00:19:59,960 --> 00:20:05,420
in Ethereum you can also express in this
extended UTxO model that Cardano uses,

253
00:20:06,170 --> 00:20:12,440
but it has a lot of important advantages
in comparison to the Ethereum model.

254
00:20:13,010 --> 00:20:19,040
So for example, in Plutus, it is
possible to check whether a transaction

255
00:20:19,070 --> 00:20:23,115
will validate in your wallet before
you ever sent it to the chain.

256
00:20:24,555 --> 00:20:29,615
So something can still go wrong, so
for example, your transaction can

257
00:20:29,615 --> 00:20:34,415
consume an output and then when it
gets to the chain, somebody else

258
00:20:34,415 --> 00:20:36,335
has already consumed that output.

259
00:20:36,845 --> 00:20:39,725
This output has already been
consumed by another transaction.

260
00:20:39,725 --> 00:20:44,615
You can't prevent that, but in that
case, your transaction will simply fail

261
00:20:44,825 --> 00:20:47,075
without you having to pay any fees.

262
00:20:47,465 --> 00:20:51,750
But if all the inputs are still
there, that your transaction expects.

263
00:20:52,050 --> 00:20:56,280
Then you can be sure that the transaction
will be validate and that it will

264
00:20:56,280 --> 00:21:00,270
have the effect that you predicted
when you ran it in your wallet.

265
00:21:01,260 --> 00:21:07,290
And this is definitely not the case in
Ethereum, in Ethereum in the time between

266
00:21:07,320 --> 00:21:11,790
you constructing the transaction and it
being incorporated into the blockchain, a

267
00:21:11,790 --> 00:21:16,770
lot of stuff can happen concurrently and
that's unpredictable, and that can have

268
00:21:16,770 --> 00:21:21,120
unpredictable effects on what will happen
when your script eventually executes.

269
00:21:21,510 --> 00:21:24,180
So that means in Ethereum it's
always possible that you have to

270
00:21:24,180 --> 00:21:29,460
pay guest fees for a transaction,
although the transaction eventually

271
00:21:29,460 --> 00:21:33,690
fails with an error, and that is
guaranteed not to happen in Cardano.

272
00:21:34,500 --> 00:21:41,350
In addition to that, it's also easier to
analyze a Plutus script and to check or

273
00:21:41,370 --> 00:21:47,010
even proof that it is secure because you
don't have to consider the whole state

274
00:21:47,010 --> 00:21:48,750
of the blockchain, which is unknowable.

275
00:21:49,230 --> 00:21:55,409
You can concentrate on this context that
just consists of the spending transaction.

276
00:21:56,070 --> 00:22:00,449
So you have a much more limited scope
and that makes it much easier to

277
00:22:00,810 --> 00:22:04,949
understand what a script is actually
doing and what can possibly happen

278
00:22:04,980 --> 00:22:06,389
or what could possibly go wrong.

279
00:22:08,129 --> 00:22:12,210
So this is it, that's the extended
UTxO model that Plutus uses.

280
00:22:12,659 --> 00:22:22,429
So to recapitulate in extending the
normal UTxO model, we replace public key

281
00:22:22,429 --> 00:22:30,129
addresses from the normal UTxO model with
scripts, Plutus scripts, and instead of

282
00:22:30,885 --> 00:22:37,245
legitimizing the consumption of new UTxO
by digital signatures, as in the simple

283
00:22:37,245 --> 00:22:43,535
UTxO model, arbitrary data it's called
redeemer is used on the input side.

284
00:22:44,355 --> 00:22:48,395
And we also add arbitrary
custom data on the output side.

285
00:22:49,575 --> 00:22:55,815
And the script as context when it
runs, sees the spending transaction,

286
00:22:55,975 --> 00:22:58,515
the transaction one, in this example.

287
00:22:59,355 --> 00:23:04,965
So given the redeemer and the datum and
the transaction with its other inputs

288
00:23:04,965 --> 00:23:10,485
and outputs, the script can run arbitrary
logic to decide whether it's okay for this

289
00:23:10,485 --> 00:23:12,465
transaction to consume the output or not.

290
00:23:13,125 --> 00:23:15,425
And that is how Plutus works.

291
00:23:17,195 --> 00:23:22,145
One thing I haven't mentioned yet
is who is responsible for providing

292
00:23:22,264 --> 00:23:27,515
datum, redeemer and the validator,
the script that validates whether

293
00:23:27,515 --> 00:23:30,365
a transaction can consume an input.

294
00:23:30,975 --> 00:23:35,415
And the rule in Plutus is that the
spending transaction has to do that

295
00:23:35,415 --> 00:23:40,004
whereas the producing transaction
only has to provide hashes.

296
00:23:40,395 --> 00:23:47,115
So that means if I produce an output
that sits at a script address, then this

297
00:23:47,145 --> 00:23:53,205
producing transaction only has to include
the hash of the script and the hash of

298
00:23:53,205 --> 00:23:55,245
the datum that belongs to this output.

299
00:23:55,635 --> 00:23:59,955
But optionally, it can include
the datum and the script as well,

300
00:24:00,314 --> 00:24:02,264
fully, but that's only optional.

301
00:24:02,985 --> 00:24:08,185
And if a transaction wants to consume such
a script output, then that transaction,

302
00:24:08,185 --> 00:24:14,145
the spending transaction has to include
the datum and the redeemer and the script.

303
00:24:14,655 --> 00:24:18,165
So that's the rule, how it works
in Plutus, which of course means

304
00:24:18,465 --> 00:24:23,355
that in order to be able to spend
a given input, you need to know

305
00:24:23,355 --> 00:24:28,784
the datum because only the hash is
publicly visible on the blockchain.

306
00:24:30,270 --> 00:24:34,080
Which is sometimes a problem and not
what you want and that's where this

307
00:24:34,140 --> 00:24:39,030
optional possibility comes into to also
include it in the producing transaction.

308
00:24:40,170 --> 00:24:44,970
Otherwise only people that know the
datum by some other means not by

309
00:24:44,970 --> 00:24:48,150
looking at the blockchain would be
able to ever spend such an output.

310
00:24:49,830 --> 00:24:55,350
So this is the UTxO model, the extended
unspent transaction output model.

311
00:24:55,980 --> 00:25:00,060
And that is of course not tied to
a specific programming language.

312
00:25:00,180 --> 00:25:05,040
I mean, what we have is Plutus, which
is based on Haskell, but in principle,

313
00:25:05,040 --> 00:25:09,600
you could use the same concept, the
same UTxO model with a completely

314
00:25:09,630 --> 00:25:11,280
different programming language.

315
00:25:11,850 --> 00:25:18,150
And we also plan to write compilers
from other programming languages to

316
00:25:18,150 --> 00:25:22,260
Plutus script which is sort of the
assembly language and aligned Plutus.

317
00:25:23,040 --> 00:25:28,395
So there's an extended UTxO model
is different from the specific

318
00:25:28,395 --> 00:25:29,745
programming language we use.

319
00:25:30,495 --> 00:25:35,145
In this course, we will use Plutus
obviously, but the understanding

320
00:25:35,145 --> 00:25:39,945
the UTxO model is independently
valid from understanding Plutus or

321
00:25:39,945 --> 00:25:41,835
learning the Plutus, Plutus syntax.

322
00:25:48,455 --> 00:25:53,735
And I planned this lecture and the
course, I first thought I, I should

323
00:25:53,764 --> 00:26:00,274
do it the traditional way of starting
very simple and maybe give a crash

324
00:26:00,274 --> 00:26:05,375
introduction into a Haskell, then
do some simple Plutus contracts and

325
00:26:05,855 --> 00:26:07,685
slowly add more complicated stuff.

326
00:26:08,135 --> 00:26:11,105
But then I decided it would be
more interesting, especially for

327
00:26:11,105 --> 00:26:16,715
the first lecture to showcase a
more interesting contract and just

328
00:26:17,014 --> 00:26:18,725
demonstrate what Plutus can do.

329
00:26:19,235 --> 00:26:24,094
And then use that to look at
certain concepts in more detail

330
00:26:24,094 --> 00:26:25,594
and explain them in more detail.

331
00:26:27,024 --> 00:26:32,814
So the code for this course we'll
be in this GitHub repository

332
00:26:33,205 --> 00:26:37,784
it's at input-outpu-hk, and
then plutus-pioneer-program.

333
00:26:37,885 --> 00:26:40,655
So I have a local clone
of this repository.

334
00:26:41,695 --> 00:26:47,430
And the code for week one is in
the sub folder code slash week one.

335
00:26:48,990 --> 00:26:53,040
And in order to build this, the
most reliable way is to use nix.

336
00:26:54,390 --> 00:26:58,980
And for that, we need the right
dependency of the Plutus repository.

337
00:26:59,520 --> 00:27:02,790
And that one is mentioned
in the cabal project file.

338
00:27:02,970 --> 00:27:08,730
So we see here in this folder, there's
this cabal project file and if we

339
00:27:08,730 --> 00:27:19,240
look at that, then here, this is the
reference to the Plutus repository, here

340
00:27:19,240 --> 00:27:22,180
you also can see the address on GitHub.

341
00:27:22,210 --> 00:27:25,470
So it's input-output-hk/plutus.

342
00:27:26,350 --> 00:27:30,550
And this is the tag we're
using for the code this week.

343
00:27:30,820 --> 00:27:33,550
So this will change during the
duration of the course because

344
00:27:33,550 --> 00:27:35,290
Plutus is still under development.

345
00:27:35,290 --> 00:27:41,085
So, stuffs has permanently changed
and I'll try to keep the lectures

346
00:27:41,115 --> 00:27:42,495
as up to date as possible.

347
00:27:42,495 --> 00:27:46,725
So probably every week I
will change this dependency.

348
00:27:47,415 --> 00:27:54,885
So once we have this, we can go to
the Plutus folder so I also have that

349
00:27:55,035 --> 00:28:02,205
locally, clone of the Plutus repository
and there we must make sure that we

350
00:28:02,205 --> 00:28:09,115
have the right hash so we can, for
example, do a git log and then this

351
00:28:09,195 --> 00:28:12,915
commit hash here must be the one that's
mentioned in the cabal project file.

352
00:28:13,245 --> 00:28:20,535
If not, we have to use, git checkout with
that hash from the cabal project file.

353
00:28:22,455 --> 00:28:29,850
And then we start the nix shell, I already
did this, so I won't execute this now.

354
00:28:29,880 --> 00:28:34,340
So I'm already in a nix shell, but
in this Plutus repository folder

355
00:28:34,360 --> 00:28:35,590
we have to start a nix shell.

356
00:28:35,940 --> 00:28:40,410
And when you do that for the first time,
it can take, take quite a while, and you

357
00:28:40,410 --> 00:28:45,240
should also consult the readme of the
Plutus repository, how to configure nix,

358
00:28:45,270 --> 00:28:49,440
because you have to use the appropriate
caches so that you don't have to

359
00:28:49,440 --> 00:28:54,690
build everything by yourself, but can
reuse the cache content then it's much

360
00:28:54,690 --> 00:28:56,460
faster, otherwise it might take hours.

361
00:28:57,240 --> 00:29:03,920
So once you have this nix shell, you
can then go back to the Plutus Pioneer

362
00:29:03,920 --> 00:29:12,480
Program repo for the appropriate week,
and then build the code with cabal build.

363
00:29:14,675 --> 00:29:19,415
And this will also take a while the first
time you do it, I did it before, so in

364
00:29:19,415 --> 00:29:24,125
that case it's instantaneous, but the
first time will take quite some time.

365
00:29:24,275 --> 00:29:30,625
So you need some patients, but that's the
most reliable way to do it and to build

366
00:29:30,625 --> 00:29:33,305
the code that's accompanying this course.

367
00:29:35,895 --> 00:29:40,245
As my introductory example, I
pick the example of an auction.

368
00:29:41,055 --> 00:29:46,605
So the idea is somebody wants to
auction an NFT, a non fungible token.

369
00:29:47,175 --> 00:29:54,675
That is a native token on Cardano
that only exists exactly once and NFT

370
00:29:54,675 --> 00:30:00,455
itself can represent some digital art
or maybe also some real world asset.

371
00:30:02,054 --> 00:30:04,965
And the owner of the token
wants to auction it away.

372
00:30:05,864 --> 00:30:11,385
And the idea is that this auction is
parameterized by the owner of the token

373
00:30:11,385 --> 00:30:14,665
and the token itself, then a minimal bid.

374
00:30:14,864 --> 00:30:19,905
So no bid below that minimum will
be accepted and the deadline.

375
00:30:19,965 --> 00:30:23,294
So all the bids have to
arrive before the deadline.

376
00:30:24,885 --> 00:30:29,445
So let's say that Alice has an
NFT and wants to auction it.

377
00:30:29,925 --> 00:30:37,215
So she creates a UTxO at the script output
where the script is the auction script.

378
00:30:37,665 --> 00:30:41,554
We will look at the code later,
but first I just want to explain

379
00:30:41,554 --> 00:30:44,015
the idea in the UTxO model.

380
00:30:45,175 --> 00:30:52,709
And the value of that UTxO is just
the NFT, and the datum at the moment

381
00:30:52,709 --> 00:30:57,010
is nothing, later it will be the
highest bidder and the highest bid.

382
00:30:57,600 --> 00:31:01,649
But right now there hasn't
been a bid, so it's nothing.

383
00:31:03,510 --> 00:31:08,669
In the real blockchain you can't have a
UTxO that just contains native tokens.

384
00:31:09,000 --> 00:31:13,080
They always have to be accompanied
by some ADA, but I'm ignoring

385
00:31:13,080 --> 00:31:14,669
this for simplicity here.

386
00:31:15,750 --> 00:31:21,989
Now let's say that Bob wants to bid
100 ADA, maybe that's the minimal bit.

387
00:31:23,070 --> 00:31:27,179
So in order to do this, Bob
creates a transaction with

388
00:31:27,360 --> 00:31:29,070
two inputs and one output.

389
00:31:29,850 --> 00:31:34,110
And the first input is the auction UTxO.

390
00:31:34,500 --> 00:31:41,459
The second input is Bob's bid, 100
ADA, and the output is again at

391
00:31:41,459 --> 00:31:46,260
the auction script, but now the
value and the datum has changed.

392
00:31:47,115 --> 00:31:51,825
So before the datum was just nothing,
because there hadn't been a bid yet.

393
00:31:52,215 --> 00:31:55,095
Now it's just Bob and a hundred.

394
00:31:55,695 --> 00:32:01,005
So it requires the highest bidder,
Bob and how high the bid was, 100.

395
00:32:01,965 --> 00:32:07,185
The value has changed because now
there's not only the NFT contained in

396
00:32:07,185 --> 00:32:11,334
this UTxO, but also the 100 ADA bid.

397
00:32:12,795 --> 00:32:19,685
And as a redeemer in order to
unlock the original auction UTxO,

398
00:32:20,715 --> 00:32:22,635
we use something called bid.

399
00:32:23,085 --> 00:32:27,450
So that's just an algebraic data
type, there would be other values as

400
00:32:27,450 --> 00:32:33,000
well but one of those is bid and the
script, the auction script will check

401
00:32:33,000 --> 00:32:35,610
that all the conditions are satisfied.

402
00:32:35,760 --> 00:32:40,830
So in this case, the script has to
check that the bid happens before the

403
00:32:40,830 --> 00:32:47,370
deadline, that the bid is high enough
higher than the minimal bid and that the

404
00:32:47,370 --> 00:32:49,080
correct inputs and outputs are there.

405
00:32:49,290 --> 00:32:55,200
So the auction is an input and also
an output that again contains the

406
00:32:55,200 --> 00:33:01,050
NFT and contains the correct highest
bid in addition to that, and that

407
00:33:01,050 --> 00:33:03,000
the datum is updated correctly.

408
00:33:03,600 --> 00:33:09,690
Next let's assume that Charlie
wants to outbid Bob and bid 200 ADA.

409
00:33:10,410 --> 00:33:13,140
So Charlie will create
another transaction.

410
00:33:13,830 --> 00:33:16,890
This time one with two
inputs and two outputs.

411
00:33:17,490 --> 00:33:24,195
So, as in the first case, the two
inputs are Charlie's bid, the 200 ADA

412
00:33:24,705 --> 00:33:32,325
and the auction UTxO and one of the
outputs is the updated auction UTxO.

413
00:33:32,925 --> 00:33:36,765
So when I say updated, recall that
I earlier said nothing ever changes.

414
00:33:37,215 --> 00:33:42,135
So the old auction UTxO is consumed
is spent and the new one is created,

415
00:33:43,335 --> 00:33:48,735
but it has this feel of updating
the state of the auction UTxO.

416
00:33:49,665 --> 00:33:52,725
Anyway, so that gets updated.

417
00:33:52,725 --> 00:33:57,945
So instead of NFT and 100 ADA will
now contain NFT and 200 ADA, then use

418
00:33:57,945 --> 00:34:01,875
higgest bid and also the datum will
reflect that now the highest bidder

419
00:34:01,875 --> 00:34:04,845
is Charlie and the highest bid is 200.

420
00:34:05,745 --> 00:34:10,995
And that will be an additional output
namely Bob will get his bid back.

421
00:34:11,895 --> 00:34:16,199
And that's also the reason, one of the
reasons we have to recall the highest

422
00:34:16,199 --> 00:34:22,169
bidder and the highest bid so that we know
who will get the old highest bid back.

423
00:34:23,279 --> 00:34:30,029
And in this case we again use the
bid redeemer, but now the script has

424
00:34:30,029 --> 00:34:35,668
to check as before that the deadline
has not been reached test to check

425
00:34:35,668 --> 00:34:39,448
that the new highest bid is actually
higher than the old highest bid.

426
00:34:40,409 --> 00:34:45,779
It has to check that the new
auction UTxO is correctly updated.

427
00:34:46,500 --> 00:34:49,960
And it also has to make sure that
the original highest bidder, Bob

428
00:34:49,980 --> 00:34:52,290
in this case gets his bid back.

429
00:34:53,100 --> 00:34:59,190
Finally, let's assume that there won't
be another bid, so once the deadline has

430
00:34:59,190 --> 00:35:02,040
been reached, the auction can be closed.

431
00:35:02,940 --> 00:35:08,220
In order to do that, somebody has to
create yet another transaction, that

432
00:35:08,279 --> 00:35:13,780
could be Alice who wants her bid or
it could also be Charlie who wants

433
00:35:13,780 --> 00:35:18,450
the NFT, it doesn't matter, it can be
anybody, but those two actually have an

434
00:35:18,450 --> 00:35:20,280
incentive to create this transaction.

435
00:35:21,510 --> 00:35:29,340
So this transaction will have one input,
just the auction UTxO with redeemer close,

436
00:35:29,640 --> 00:35:32,670
not bid in this case and two outputs.

437
00:35:33,180 --> 00:35:37,950
And one of the outputs is the
highest bidder, Charlie, and he

438
00:35:37,950 --> 00:35:39,720
gets the NFT, he won the auction.

439
00:35:39,720 --> 00:35:45,390
So he gets what was auctioned away
and Alice, the owner of the auction,

440
00:35:45,390 --> 00:35:47,190
the original owner of the NFT.

441
00:35:47,520 --> 00:35:54,980
She gets the highest bid and that closes
the auction and finished this scenario.

442
00:35:55,640 --> 00:36:00,230
And the script in the close case
has to check that the deadline has

443
00:36:00,230 --> 00:36:05,480
been reached and that the highest
bidder gets the NFT and that the

444
00:36:05,480 --> 00:36:07,160
auction owner gets the highest bid.

445
00:36:08,880 --> 00:36:14,560
There's one more scenario for us to
consider namely that nobody made any bid.

446
00:36:15,330 --> 00:36:19,480
So, Alice starts the auction,
but then nobody creates a bid.

447
00:36:21,210 --> 00:36:26,609
And in this case, there must be a
mechanism for Alice to retrieve her NFT.

448
00:36:27,240 --> 00:36:30,720
So for that, she creates a transaction
again with the close redeemer.

449
00:36:31,259 --> 00:36:36,390
But now, because there is no bidder,
the NFT doesn't go to the highest

450
00:36:36,390 --> 00:36:40,650
bidder because there is no highest
bidder, but simply goes back to herself.

451
00:36:41,100 --> 00:36:45,779
So the logic in this case, if there's
no highest bidder is likely different

452
00:36:45,779 --> 00:36:52,149
for the close redeemer, it must check
that the NFT goes back to Alice.

453
00:36:52,890 --> 00:36:55,740
Actually, it doesn't have to
check anything because I mean,

454
00:36:55,770 --> 00:36:57,160
this will be triggered by Alice.

455
00:36:57,160 --> 00:36:58,920
Alice will create this transaction.

456
00:36:59,250 --> 00:37:02,009
And of course she could send
the NFT wherever she wants.

457
00:37:03,745 --> 00:37:07,435
Let's have a brief look at the code,
but don't worry, I don't expect

458
00:37:07,435 --> 00:37:09,295
you to understand it at this point.

459
00:37:10,995 --> 00:37:14,835
It's an important thing to realize
about Plutus is that there's

460
00:37:14,865 --> 00:37:16,485
on-chain and off-chain code.

461
00:37:17,385 --> 00:37:21,375
On-chain code is this script
we were discussing in the

462
00:37:21,395 --> 00:37:23,225
script from the UTxO model.

463
00:37:23,435 --> 00:37:30,365
So in addition to public key addresses,
we have script addresses and outputs

464
00:37:30,395 --> 00:37:32,165
can sit at such a script address.

465
00:37:32,195 --> 00:37:39,035
And if a transaction tries to consume such
an output, the script is executed and only

466
00:37:39,035 --> 00:37:41,795
if it succeeds, the transaction is valid.

467
00:37:42,695 --> 00:37:49,295
So how it works is if a node receives
a new transaction, it validates

468
00:37:49,295 --> 00:37:53,585
it before accepting it into its
mempool and eventually into a block.

469
00:37:54,335 --> 00:37:59,025
And for each input of the transaction,
if that input happens to be a

470
00:37:59,025 --> 00:38:04,995
script address, the corresponding
script is executed and must succeed.

471
00:38:05,445 --> 00:38:08,475
And if it doesn't succeed, then
the transaction is invalid.

472
00:38:09,045 --> 00:38:14,775
So that's the so-called on-chain
aspect of Plutus and the programming

473
00:38:14,775 --> 00:38:20,595
language this script is expressed in as
written in is called Plutus core, but

474
00:38:20,595 --> 00:38:25,605
you never write plutus core by hand,
instead you write Haskell and then

475
00:38:25,665 --> 00:38:27,765
that gets compiled down to Plutus core.

476
00:38:28,275 --> 00:38:33,045
And eventually there may also very well be
other higher level programming languages,

477
00:38:33,075 --> 00:38:39,765
like maybe solidity or C or Python that
can compile it down to Plutus core.

478
00:38:41,475 --> 00:38:46,845
So that's the one thing that's the
script and the task of a script is to say

479
00:38:46,845 --> 00:38:52,125
yes or no can this transaction consume
the output I'm locking, yes or no?

480
00:38:52,905 --> 00:38:56,685
But in order to actually
use such an output that is

481
00:38:56,685 --> 00:38:58,005
locked at the script address.

482
00:38:58,245 --> 00:39:03,055
So in order to create a transaction
that will unlock section output and

483
00:39:03,055 --> 00:39:08,835
use that input, you of course must
be able to construct a transaction

484
00:39:09,075 --> 00:39:10,875
that will then pass validation.

485
00:39:11,895 --> 00:39:15,945
And that is the responsibility
of the off-chain part of Plutus.

486
00:39:16,635 --> 00:39:20,175
So there is a part that runs in
the wallet, not on the blockchain,

487
00:39:20,715 --> 00:39:25,245
and that will construct suitable
transactions that are then able

488
00:39:25,545 --> 00:39:28,575
to unlock a given script output.

489
00:39:29,310 --> 00:39:32,970
So that's like a dual role of
on-chain and off-chain, on chain

490
00:39:33,030 --> 00:39:36,300
checks and validates, it doesn't do
anything, it just says yes or no.

491
00:39:36,900 --> 00:39:41,400
And the off-chain part constructs
actively creates a transaction

492
00:39:41,580 --> 00:39:43,410
that will then pass validation.

493
00:39:44,640 --> 00:39:48,060
And the nice thing, or one of the
nice things about Plutus is that

494
00:39:48,390 --> 00:39:52,110
both the on-chain and the off-chain
parts are written in Haskell.

495
00:39:52,320 --> 00:39:56,070
So one obvious advantage of that
is that you don't have to learn two

496
00:39:56,070 --> 00:39:58,930
programming languages, just one Haskell.

497
00:39:59,730 --> 00:40:03,930
And the other advantage is
that you can share code between

498
00:40:04,020 --> 00:40:05,250
on-chain and off-chain part.

499
00:40:05,730 --> 00:40:09,780
Later in this course we will talk about
state machines, then this aspect is

500
00:40:09,780 --> 00:40:15,210
even more direct, there you can really
use the same, literally the same code,

501
00:40:15,360 --> 00:40:18,030
both for checking and for construction.

502
00:40:18,600 --> 00:40:23,210
But even if you don't use state
machines there's still a lot

503
00:40:23,210 --> 00:40:26,430
of possibility to share code.

504
00:40:27,000 --> 00:40:31,919
So if we briefly look at the code, so
here, for example, it's just a Haskell

505
00:40:31,919 --> 00:40:34,260
data type that defines an auction.

506
00:40:34,260 --> 00:40:38,010
So it's the seller, the deadline,
the minimal bid and then the last

507
00:40:38,010 --> 00:40:46,940
two define the NFT and various
other data types .And here, this

508
00:40:46,940 --> 00:40:49,310
is the heart of the on-chain code.

509
00:40:49,430 --> 00:40:54,290
So this defines the script, the logic
of the script, that validates where the

510
00:40:54,350 --> 00:41:00,800
transaction is allowed to spend a given
output sitting at this auction contract.

511
00:41:01,370 --> 00:41:04,650
So there are various helper
functions here to do that.

512
00:41:05,640 --> 00:41:09,500
And so this is that.

513
00:41:10,790 --> 00:41:14,840
And then here, this is where
the compilation happens.

514
00:41:14,960 --> 00:41:19,520
So the, this functionary address
shorter it's just Haskell, but

515
00:41:19,520 --> 00:41:23,180
then here you have something called
template Haskell to activate the

516
00:41:24,240 --> 00:41:28,730
GHC plug in that then compiles,
this Haskell code to Plutus core.

517
00:41:29,830 --> 00:41:37,420
And here the off-chain part starts,
which defines various parameters for

518
00:41:37,730 --> 00:41:40,540
endpoints that can be then invoked.

519
00:41:40,810 --> 00:41:44,770
So we have three endpoints for
this example, start will be used

520
00:41:44,770 --> 00:41:50,050
by the seller to start the auction,
to log the NFT into the auction

521
00:41:50,920 --> 00:41:53,680
contract and then bid and close.

522
00:41:53,680 --> 00:41:57,910
So bid obviously will be used by
bidders to make a bid and close

523
00:41:57,910 --> 00:42:02,470
will be used either by the winner
of the auction or by the seller.

524
00:42:04,109 --> 00:42:10,750
And so here, these operations are
defined, so this is the start logic.

525
00:42:11,710 --> 00:42:15,160
Then we have the bid logic here.

526
00:42:18,415 --> 00:42:18,835
Okay.

527
00:42:19,004 --> 00:42:22,084
That's a bit further and then
finally here, the close logic.

528
00:42:23,555 --> 00:42:29,214
And then some helper functions and this
just basically packages everything up.

529
00:42:29,935 --> 00:42:33,475
It says, okay, we will have these
three endpoints start, bid and close.

530
00:42:34,254 --> 00:42:35,995
And they are called start, bid and close.

531
00:42:36,384 --> 00:42:42,205
And the last lines are just for demo
purposes or for trying it out in

532
00:42:42,205 --> 00:42:47,785
the playground to create an sample
NFT that we can use to auction away.

533
00:42:47,875 --> 00:42:51,145
So that has nothing to do
with the actual contract.

534
00:42:52,435 --> 00:42:56,275
And what I said about code reuse,
for example, if you look here

535
00:42:56,275 --> 00:43:02,125
at the bid off-chain part that
uses a function min bid here.

536
00:43:04,380 --> 00:43:08,250
Basically determines giving on the
current datum on the state of the

537
00:43:08,250 --> 00:43:13,990
contract, whether there was already a
bid or not, determines the minimal bid.

538
00:43:14,490 --> 00:43:22,620
And if we look for that, we
see that this is defined here.

539
00:43:24,640 --> 00:43:28,650
And it's also used here we
are in the on-chain part.

540
00:43:29,460 --> 00:43:33,360
So obviously this script must
check if a new bid comes in,

541
00:43:33,390 --> 00:43:34,470
whether it's high enough.

542
00:43:34,740 --> 00:43:38,880
So it's useful to have function that
computes this minimal bid but also in

543
00:43:38,880 --> 00:43:43,500
the off-chain part where I'm back to
now, it's also useful if the wallet

544
00:43:43,500 --> 00:43:47,190
before even bother us constructing a
transaction that makes a bid, checks

545
00:43:47,190 --> 00:43:48,510
whether the bid is high enough.

546
00:43:48,960 --> 00:43:52,770
That's not strictly speaking
necessary, the wallet could just

547
00:43:53,010 --> 00:43:56,920
construct the transaction anyway,
but then it would be doomed to fail.

548
00:43:57,220 --> 00:44:01,379
So it would be stupid to actually
construct it in the first place.

549
00:44:01,740 --> 00:44:04,920
That's why I have this check
in here that checks whether the

550
00:44:05,110 --> 00:44:06,480
bid is actually high enough.

551
00:44:07,350 --> 00:44:11,430
But the point I want to make is that
this min bid helper function can be

552
00:44:11,430 --> 00:44:15,270
shared between on-chain and off-chain
code because it's just a plane

553
00:44:15,270 --> 00:44:19,680
Haskell function and can be used in
both parts of the Plutus contract.

554
00:44:21,060 --> 00:44:24,779
So that's a very nice aspect of
Plutus that you don't have code

555
00:44:24,779 --> 00:44:29,580
duplication between the on-chain part
that lives on the blockchain and this

556
00:44:29,910 --> 00:44:34,650
responsible for validation and the
off-chain part that runs in the user's

557
00:44:34,680 --> 00:44:40,109
wallet on the user's local machine,
or later in the user's web browser.

558
00:44:40,710 --> 00:44:46,690
And it's used to construct transactions
that will then pass a validation.

559
00:44:47,610 --> 00:44:53,280
So it's important to keep these two uses
apart and then to realize what they are.

560
00:44:53,420 --> 00:44:57,560
And sometimes it's confusing when
people talk about smart contracts

561
00:44:57,660 --> 00:44:59,220
or contracts, what do they mean?

562
00:44:59,250 --> 00:45:02,250
do they mean the script,
the on-chain script?

563
00:45:02,640 --> 00:45:07,200
Or do they mean the off-chain part that
lives in the wallet and run some wallet?

564
00:45:07,200 --> 00:45:10,200
And it's even more confusing because
the Haskell data type used for the

565
00:45:10,200 --> 00:45:12,090
off-chain part is also called contract.

566
00:45:12,750 --> 00:45:16,980
So if you talk about contract, do
you mean this capital C contract,

567
00:45:17,130 --> 00:45:21,990
the off-chain contract that's
executed in, on the user's machine?

568
00:45:23,130 --> 00:45:24,720
Or do we talk about something else?

569
00:45:24,840 --> 00:45:28,350
So it's important to be precise
about what we actually mean

570
00:45:28,350 --> 00:45:29,490
when we discuss something.

571
00:45:30,900 --> 00:45:31,140
Yes.

572
00:45:31,140 --> 00:45:35,250
But just to summarize, so we have
on-chain and off-chain, on-chain gets

573
00:45:35,280 --> 00:45:43,880
compiled down to Plutus core and is
living on the blockchain and is executed

574
00:45:43,880 --> 00:45:45,855
by nodes that validate transactions.

575
00:45:46,665 --> 00:45:51,075
And if you have the off-chain code
that lives on the user's machine

576
00:45:51,465 --> 00:45:55,665
and is responsible for constructing
transactions and submitting transactions,

577
00:45:55,665 --> 00:46:01,225
that will then unlog certain script
outputs and both are written in Haskell.

578
00:46:01,245 --> 00:46:07,135
And that allows us to share code between
them, which avoids code duplication.

579
00:46:08,005 --> 00:46:12,465
So we have a shorter code and
basically guaranteed that the parts

580
00:46:12,495 --> 00:46:16,245
fit together or these it's easier
to make the parts fit together.

581
00:46:17,805 --> 00:46:23,025
Now, we want to try this in the
playground and we won't use the publicly

582
00:46:23,025 --> 00:46:28,425
available playground because that's
outdated, that's from February I believe.

583
00:46:29,085 --> 00:46:32,895
We want to use one that is
in sync with the version of

584
00:46:32,895 --> 00:46:34,365
Plutus we are using right now.

585
00:46:35,025 --> 00:46:41,660
So we go back to the Plutus
repository in a nix shell to the

586
00:46:41,940 --> 00:46:45,380
sub folder plutus-playground-client.

587
00:46:46,180 --> 00:46:53,910
And we start
plutus-playground-server there.

588
00:47:00,640 --> 00:47:07,720
Then we go to a different console,
but the same folder again in the

589
00:47:07,720 --> 00:47:14,200
nix shell and we do npm start
to start the playground client.

590
00:47:20,270 --> 00:47:27,020
And then we can open this address in a
browser and find our playground there.

591
00:47:29,069 --> 00:47:34,049
So first we would see the editor
window and we can just take the code

592
00:47:34,109 --> 00:47:36,120
we just looked at and paste it in here.

593
00:47:36,930 --> 00:47:40,710
And press compile to compile it
and if all goes well, that should

594
00:47:40,710 --> 00:47:42,390
compile without error message.

595
00:47:45,620 --> 00:47:50,830
It does, now we can go to simulate
and here we have simulated

596
00:47:50,860 --> 00:47:53,120
wallets and can invoke endpoints.

597
00:47:53,770 --> 00:47:57,310
So by default, there are only two
wallets, but if you want to replay the

598
00:47:57,310 --> 00:48:02,770
scenario I showed in the UTxO diagram,
you should create a third wallet.

599
00:48:04,180 --> 00:48:07,900
And we see that by default, the
opening balances are just 10

600
00:48:07,900 --> 00:48:13,640
lovelace and 10 of this token, but
I want this token to be an NFT.

601
00:48:14,030 --> 00:48:16,750
So that doesn't make any sense anyway.

602
00:48:17,140 --> 00:48:21,190
So let's say wallet one is Alice, wallet
two is Bob and wallet three is Charlie.

603
00:48:21,850 --> 00:48:26,570
So Alice has the one T and that's
the only one we have, so for the

604
00:48:26,570 --> 00:48:31,720
other say zero and 10 lovelace,
is of course, ridiculously low.

605
00:48:31,779 --> 00:48:38,335
So make that, I don't know, a thousand
ADA, so one ADA is a million lovelace.

606
00:48:38,355 --> 00:48:40,905
So 1, 2, 3, 1, 2, 3.

607
00:48:41,635 --> 00:48:43,275
Let's give everybody the same.

608
00:48:48,315 --> 00:48:50,715
Okay, so now we can invoke endpoints.

609
00:48:50,735 --> 00:48:53,745
So Alice starts the auction.

610
00:48:54,805 --> 00:48:57,855
We have to provide parameters,
the first one is the deadline.

611
00:48:59,205 --> 00:49:05,175
Let's say the deadline is slot 10,
but time is measured in posix time.

612
00:49:05,175 --> 00:49:11,065
So in seconds from 1st of January
1970 I believe, something like that.

613
00:49:12,015 --> 00:49:16,155
So it's not so clear what
value makes sense there.

614
00:49:17,235 --> 00:49:25,245
Luckily in the plutus-ledger
package in module Ledger.TimeSlot.

615
00:49:25,605 --> 00:49:29,145
There's a convenient
function slot to posix time.

616
00:49:29,805 --> 00:49:33,810
So if we import that in the repl.

617
00:49:37,859 --> 00:49:42,450
Now we have this slot to posix
time and if we need to slot

618
00:49:42,480 --> 00:49:47,520
10, you get this value here.

619
00:49:49,509 --> 00:49:55,190
Probably I think the simulation always
start at the beginning of the Shelley era.

620
00:49:55,940 --> 00:50:02,760
So probably if you convert it, it
will be sometime, some of 2020, but

621
00:50:02,760 --> 00:50:04,680
in any case, we can use this value.

622
00:50:05,580 --> 00:50:07,110
So let's use the value here.

623
00:50:08,100 --> 00:50:13,380
Now the minimum bid, let's say
100 ADA, and now we must specify

624
00:50:13,380 --> 00:50:15,070
the NFT that's being auctioned.

625
00:50:15,480 --> 00:50:21,330
And because of how I set it
up, this is six, six and T.

626
00:50:21,750 --> 00:50:23,340
So don't worry about the 66.

627
00:50:23,400 --> 00:50:27,210
That's just how this T was defined.

628
00:50:28,770 --> 00:50:29,010
Okay.

629
00:50:29,010 --> 00:50:31,320
Now let's wait one block.

630
00:50:32,705 --> 00:50:35,585
Now let's Bob make his bit.

631
00:50:36,585 --> 00:50:41,065
So this is again, specify
the NFT so it's 66 T.

632
00:50:41,685 --> 00:50:47,825
Now the bid, 100 ADA, we
wait for another block.

633
00:50:49,215 --> 00:50:55,555
Now, Charlie outbids Bob,
again the 66 and the T.

634
00:50:59,145 --> 00:51:00,735
And now 200 ADA.

635
00:51:04,425 --> 00:51:09,525
We wait until the deadline has
been reached, let's wait until just

636
00:51:09,525 --> 00:51:11,295
for good measure until slot 11.

637
00:51:11,475 --> 00:51:13,935
I'm not sure whether 10 would suffice.

638
00:51:13,935 --> 00:51:17,415
It depends how exactly before and
after the deadline is defined.

639
00:51:18,985 --> 00:51:24,100
And then Alice or Bob or Charlie,
anybody can invoke close, but Bob

640
00:51:24,120 --> 00:51:28,220
has no reason to, so it would be
Alice or Charlie,  let's say Alice.

641
00:51:28,290 --> 00:51:36,920
So she invokes the close endpoint,
again 66 T and let's wait for one

642
00:51:36,920 --> 00:51:40,640
more block and let's evaluate.

643
00:51:44,980 --> 00:51:49,980
Okay, and now we see the
transactions that were simulated.

644
00:51:50,050 --> 00:51:55,410
We see there were 1, 2, 3, 4, 5,
which at first glance is a bit weird

645
00:51:55,410 --> 00:51:58,890
because we only have start, two bids
and the close, so it should be four.

646
00:51:59,280 --> 00:52:01,740
But the first one in slot zero
is always there, that's the

647
00:52:01,740 --> 00:52:03,420
so-called genesis transaction.

648
00:52:03,810 --> 00:52:09,660
It's a transaction without input that
provides the initial funds to the wallets.

649
00:52:10,020 --> 00:52:15,540
So we have these three outputs for our
three wallets and we get what we specified

650
00:52:16,020 --> 00:52:24,315
so, Alice gets 1,000 ADA and the token
and two and three Bob and Charlie only

651
00:52:24,315 --> 00:52:27,285
get 1,000 ADA but nothing of the token.

652
00:52:28,095 --> 00:52:31,515
So this is the Genesis transaction
that always happens to kick things

653
00:52:31,515 --> 00:52:33,345
off and provide initial funds.

654
00:52:34,755 --> 00:52:37,725
So now in slot one, this should
be the start transaction.

655
00:52:39,195 --> 00:52:46,235
So input we see is the only UTxO
that Alice owns the her 1,000 ADA.

656
00:52:47,945 --> 00:52:51,885
And the, it contains
1,000 ADA and the NFT.

657
00:52:52,575 --> 00:52:54,375
So this is the start transaction.

658
00:52:55,095 --> 00:53:01,020
We see that fees are taken into account
here in the playground, but not properly.

659
00:53:01,380 --> 00:53:04,080
I think there's always at
the moment a flat rate of 10

660
00:53:04,080 --> 00:53:06,300
lovelace, which is not realistic.

661
00:53:06,300 --> 00:53:10,350
So in, in the real blockchain, in the
real system, the fee will of course

662
00:53:10,350 --> 00:53:15,360
depend on the transaction, how big it
is and how long the scripts run, how

663
00:53:15,360 --> 00:53:17,460
many resources they consume and so on.

664
00:53:17,970 --> 00:53:20,130
But for now the fees always 10 lovelace.

665
00:53:21,300 --> 00:53:25,260
Then the second output
here is Alice's change.

666
00:53:25,530 --> 00:53:29,640
So she gets her 1,000 ADA back
minus the 10 lovelace fee.

667
00:53:30,600 --> 00:53:34,140
And the third output is the interesting
one that goes to the auction script.

668
00:53:34,410 --> 00:53:37,650
So now the NFT is logged
in the auction script.

669
00:53:38,880 --> 00:53:42,250
So now if we go to the next
transaction, that should be Bob's bid.

670
00:53:43,500 --> 00:53:47,010
So we have two inputs as in the
diagram we looked at earlier.

671
00:53:47,010 --> 00:53:54,060
So one is the auction script with the
NFT and one is Bob's original UTxO.

672
00:53:55,250 --> 00:54:01,015
And as outputs, so we're gonna
have the fees or which in this

673
00:54:01,015 --> 00:54:02,365
case are not just 10 lovelace.

674
00:54:02,385 --> 00:54:04,345
So now we have like a higher fee.

675
00:54:05,005 --> 00:54:07,995
So it seems that changed since
last time we looked at it.

676
00:54:07,995 --> 00:54:12,385
So now it's not a flat rate
of 10 lovelace there is some

677
00:54:12,415 --> 00:54:13,945
more sophistication going on.

678
00:54:15,145 --> 00:54:17,935
The second output is Bob's change.

679
00:54:18,325 --> 00:54:25,195
So it's basically a 1,000 ADA minus the
130 bids, but then also minus the fee.

680
00:54:25,825 --> 00:54:28,495
The third output is the updated script.

681
00:54:28,735 --> 00:54:33,245
So the updated script now
contains the token and Bob's bid.

682
00:54:35,005 --> 00:54:38,955
Now let's look at the next
transaction, the Charlie's bid.

683
00:54:39,495 --> 00:54:41,925
So it's similar here on the input side.

684
00:54:42,345 --> 00:54:47,895
So the script UTxO goes in, that at the
moment contains the NFT and Bob's bid.

685
00:54:48,735 --> 00:54:52,155
Then Charlie's UTxO is the second input.

686
00:54:52,515 --> 00:54:56,265
Now we have one output more
because Bob gets his bid back.

687
00:54:56,265 --> 00:55:02,205
So we have the fees, we
have the change for Charlie.

688
00:55:02,505 --> 00:55:07,485
So he gets roughly 800 ADA change
because he, his bid was 200.

689
00:55:08,715 --> 00:55:12,925
Then we have the script output, so
the NFT is still there, but now there

690
00:55:12,985 --> 00:55:15,585
are 200 ADA in it Charlie's bid.

691
00:55:16,185 --> 00:55:23,535
And finally for wallet two for Bob, Bob
gets his 100 bid back and the last one

692
00:55:23,535 --> 00:55:25,375
will be the close, invoked by Alice.

693
00:55:26,595 --> 00:55:31,125
So input is just Alice's wallet,
this is in order to pay for the

694
00:55:31,125 --> 00:55:36,075
fees and then the script output.

695
00:55:37,185 --> 00:55:40,045
And so we have the fees,
we have changed for Alice.

696
00:55:40,065 --> 00:55:44,025
So it's virtually the same
that went in minus these fees.

697
00:55:45,705 --> 00:55:51,945
Then Alice gets the highest bid
the 200 ADA and Bob gets the token.

698
00:55:52,455 --> 00:55:54,585
So the auction has finished.

699
00:55:55,845 --> 00:55:59,865
We could check what happens
if something goes wrong.

700
00:55:59,925 --> 00:56:06,355
Or for example, if Charlie's bid is too
low, is not higher than, than Bob's bid.

701
00:56:07,455 --> 00:56:08,235
So where is it?

702
00:56:08,235 --> 00:56:12,884
That was here, the bid was 200, so
let's say Charlie makes a mistake and

703
00:56:12,884 --> 00:56:16,395
only bids instead of 200, only 20 ADA.

704
00:56:17,645 --> 00:56:19,245
So if we now evaluate.

705
00:56:23,665 --> 00:56:27,175
Okay, then we see we have
one transaction less.

706
00:56:27,865 --> 00:56:35,430
So, this is still Bob's bid with the 100,
but now Charlie's transaction was invalid.

707
00:56:35,490 --> 00:56:40,620
So that's rejected and the close
now looks different because

708
00:56:40,620 --> 00:56:41,970
now Bob is the highest bidder.

709
00:56:41,980 --> 00:56:46,530
So Alice only gets 100
and Bob gets the NFT.

710
00:56:47,730 --> 00:56:52,120
Finally, we can try what happens if there
is no valid bids So, for example, we

711
00:56:52,120 --> 00:56:59,780
can just remove the bids all together,
let's remove Bob's bid and Charlie's bid.

712
00:57:02,850 --> 00:57:06,960
And we must just wait until the deadline
has been reached, so wait until slots

713
00:57:07,260 --> 00:57:10,530
11 let's say and see what happens now.

714
00:57:14,470 --> 00:57:14,830
Okay.

715
00:57:14,830 --> 00:57:21,670
So we have the genesis transaction and
the opening of the auction and no bids.

716
00:57:22,120 --> 00:57:32,069
And now the closing of the auction will
just return the NFT here to Alice, so

717
00:57:32,069 --> 00:57:37,410
in this case, there are two outputs to
Alice's address, but in any case, she

718
00:57:37,410 --> 00:57:39,960
ends up with the NFT back in her hands.

719
00:57:40,740 --> 00:57:45,210
So you can see that this is a
relatively complex contract and one

720
00:57:45,210 --> 00:57:49,500
that might actually be useful in
practice, and it seems to work and we

721
00:57:49,500 --> 00:57:51,420
can play with it in the playground.

722
00:57:54,089 --> 00:57:58,470
So I hope you enjoyed this walk
through through the auction contract.

723
00:57:58,950 --> 00:58:03,930
And I excited to learn how to do things
like that, or even more interesting things

724
00:58:03,990 --> 00:58:06,569
like that yourself during this course.

725
00:58:07,509 --> 00:58:10,109
And that's the end of today's lecture.

726
00:58:10,290 --> 00:58:12,990
So all that remains is homework.

727
00:58:13,080 --> 00:58:18,930
So I've planned to give you a little
bit of homework every week so that

728
00:58:18,930 --> 00:58:23,430
you can practice because in learning a
programming language, it's always very

729
00:58:23,430 --> 00:58:25,480
important that you try it yourself.

730
00:58:25,800 --> 00:58:30,210
Because often, if you listen to a
lecture, even if you think you understand

731
00:58:30,210 --> 00:58:36,390
everything then if you sit down and
try it yourself, you actually realize

732
00:58:36,930 --> 00:58:40,710
if there are certain things you didn't
really understand, as well as you

733
00:58:40,800 --> 00:58:43,230
thought you did when you listened to it.

734
00:58:44,490 --> 00:58:47,580
But of course we haven't
really learned anything yet.

735
00:58:47,610 --> 00:58:50,520
So I can't ask you to write
a simple Plutus contract.

736
00:58:50,850 --> 00:58:55,620
So for the first week, I would just
like to ask you to basically do

737
00:58:55,620 --> 00:58:57,480
what I did in this walk through.

738
00:58:57,690 --> 00:59:05,770
So clone the Plutus Pioneer Program
repository, get it to build with cabal

739
00:59:05,770 --> 00:59:12,020
build, clone the Plutus repository,
check out the right commit, get the

740
00:59:12,020 --> 00:59:16,810
nix shell working, start the Plutus
playground server, start the Plutus

741
00:59:16,830 --> 00:59:21,750
playground client, then copy paste
the code from the Plutus Pioneer

742
00:59:21,750 --> 00:59:24,510
Program repo into the playground.

743
00:59:25,290 --> 00:59:30,149
And make it compile and then
simulate some auctions scenarios.

744
00:59:31,410 --> 00:59:35,700
So it would be great if, if all of you
could manage to get that working, because

745
00:59:35,700 --> 00:59:40,470
then it means that your environments
are properly set up and we're ready

746
00:59:40,470 --> 00:59:42,750
to take on more interesting things.

747
00:59:43,709 --> 00:59:45,930
So that was it for the first week.

748
00:59:46,290 --> 00:59:51,750
Thank you very much again, for attending
the course and talk to you next week.

749
00:59:52,379 --> 00:59:52,799
Thank you.

