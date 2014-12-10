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
   - uses 'btcctl' from conformal's btcd at https://github.com/conformal/btcd.git

  Example 1:

    spendbtc -n -o 12345:70,12346:10,12347:20 -b f12345 -t 0.03

  Example 2:
    $HOME/.spendbtc.conf

	my @outputs_example1 = (
		"12345:10%",
		"12392:90%"
	);

    spendbtc -n -c $HOME/.spendbtc.conf



Donations: 1HeSyCxcMvmaZg3CyqSthrqgm6fwdREqfG
