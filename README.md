Random utilities for interacting with bitcoin rpc.

 spendbtc:
   - scenario1:
     - send all unsepent input (minus a blacklist of transactions)
     - send to 10% addr1 90% addr2
   - scenario2:
     - send 50% unspent input (minus a blacklist of transactions)
     - send to 10% addr1 10% addr2 80% addr3
   - permits setting txfee (since it uses the send/sign/create rawtransaction
     rpc calls
   - cli utility
   - uses 'btcctl' from conformal's btcd at https://github.com/btcsuite/btcd.git

  Example 1:

    spendbtc -n -o 12345:70,12346:10,12347:20 -b f12345 -t 0.03

  Example 2:
    $HOME/.spendbtc.conf

	$usdperbtc = 14000.00;

	%walletcmds = (
		"fdc" => "btcctl -C ~/.btcctl/btcctl-example.conf",
	);

	# www.cointape.com is a good place to guess what to set this to
	$feepb = "0.00000030";

	# in the event btcwallet is confused and/or we want to avoid some tx'en
	# for whatever reason
	@txblacklist = (
		# "b12345....6",
	);

	my @outputs_example1 = (
		"b1234..5:10%",
		"b1239..2:90%"
		"b1245..5:0.001", # taken off the top then %'age for above
	);
	@outputs = @outputs_example1;

    spendbtc -n -c $HOME/.spendbtc.conf

NOTES:

# actually does require you to unlock your wallets prior to running.

# actually does create real live transctions so be wary of putting the wrong address in your conf files.

# remove '-n' when you are confident this is going to do what you want

# creates a 'sendtx.log' file with all transactions appended in the event retransmission is warranted, for example... I frequently do the fun trick:

	tail -1 sendtx.log | sed 's/send/decode/' | sh | less

Donations: bitcoin:1HeSyCxcMvmaZg3CyqSthrqgm6fwdREqfG
