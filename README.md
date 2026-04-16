Adatvédelmi és adatintegritási primitívek gyűjteménye, amelyek a tanítási adatok és az inferencia-folyamat védelmét biztosítják.

PaillierKeyPair: Paillier homomorf titkosítási kulcspár generálása. Két véletlenszerű 128 bites prímből (p, q) számítja n = p*q, n² = n*n, g = n+1, lambda = lcm(p-1, q-1), mu = lambda⁻¹ mod n. A kulcsgenerálás u256 és u512 aritmetikát használ.

HomomorphicEncryption: Paillier-sémán alapuló homomorf titkosítás. Az encrypt() egy i64 értéket kódol: előjelbit + abszolút érték, majd g^m * r^n mod n² formában titkosítja. A decrypt() visszafejti. Az add() titkosított összeadást végez (szorzás mod n²), a multiplyScalar() titkosított skalárszorzást (hatványozás mod n²). A kulcsok törlése secureZero-val történik (volatile write).

DatasetFingerprint: LSH (Locality-Sensitive Hashing) alapú hasonlóság-detektálás. Minden mintát Blake3-mal hash-el, a feature-vektorokat homomorf titkosítással tárolja. A checkSimilarity() 8 LSH-függvénnyel keres hasonló mintákat, Hamming-távolság < 32 esetén pozitívnak tekinti.

SecureDataSampler: k-anonimitást és differenciális adatvédelmi büdzsét betartó mintavételező. A sampleWithKAnonymity() Fisher-Yates shuffle-lel véletlenszerűen választ, és levonja a lekérdezés költségét a büdzséből.

ProofOfCorrectness: Merkle-fa alapú számítási nyomkövetés. Minden lépésnél (recordStep) Blake3-mal hash-eli a bemenetet és kimenetet, és lánc-hash-t tart fenn. A finalize() Merkle-fát épít a lépésekből, majd a Merkle-gyökérből és a lánc-hash-ből végső elköteleződést számol.

DatasetIsolation: hozzáférési korlátokat és naplózást biztosító izolációs barrier. Minden adathalmazhoz IsolationBarrier-t hoz létre véletlenszerű hozzáférési kulccsal, lejárati idővel, max hozzáférési számmal és rate-limittel. A logAccess() minden hozzáférést rögzít Blake3-mal hash-elt operáció- és kliens-azonosítóval.
