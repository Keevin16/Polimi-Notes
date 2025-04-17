>Take one or more **attributes** of the [[Documents]] and use them as [[Shard key]], in this way the value of that attribute is the **discriminator** for deciding **where to put** the [[Documents]]

  

Ex: shard_key = age

- Documents whose age is between 0 and 20 ⇒ shard 1
- Documents whose age is between 20 and 30 ⇒ shard 2
- Documents whose age is between 30 and +∞ ⇒ shard 3
- If the document does not have an age attribute ⇒ shard 4

  

NOTE: (improving performance)
	Choice of the [[Shard key]] is on us.
	Choose a [[Shard key]] that aligns with the most common query patterns ⇒ queries that include the shard_key can directly target the correct [[Shard]] 


DOWNSIDE: 
	**distribution** problem: if the attribute value of the shard key follows a distribution, then some shard will be full while others empty ⇒ even if I fix this I can not guarantee it will remains like this

#MongoDB