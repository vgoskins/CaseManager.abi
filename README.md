## API

**CaseManager#requestPurchase(uint64 userId, uint32 caseId, uint32 quantity, address affiliate) return uint256**

_Method. Requests an item purchase from case caseId. Call this method to generate a new item_

* @param userId [uint64] the external userId to associate with this purchase. Must be Luhn style checksummed
* @param caseId [caseId] the case id to select the sku from
* @param quantity [uint32] the number of items to purchase in this request. Value sent must be quantity * weiValue, and quantity must be >= 10
* @param affiliate [address] the address of the affiliate use address(0) if none
* @return [uint256] the order id for this request. Must be held on to in order to complete the purchase

**CaseManager.Events#PurchaseCreated(uint256 indexed _orderId, uint256 _blockNumber, uint64 _userId, uint32 _caseId, uint32 _quantity)**

_Event. Indicates that a purchase request has actually been created. Use this to recover the orderId to get purchase results via the getPurchaseResult method_

* _orderId [uint256] the order id for the purchase request made. Use this with the getPurchaseResult or getOrderDetails methods
* _blockNumber [uint256] the block number to use for the block hash in the getPurchaseResult method
* _userId [uint64] the external userId associated with this purchase
* _caseId [uint32] the case id selected from
* _quantity [uint32] the number of items requested for purchase at once from this case

**CaseManager#getOrderDetails(uint256 orderId) returns (uint64, uint32, uint32, uint256)**

_Method. Gets the order details without purchased item selections. This is a convenience method that can be used to get essentially the same info as the PurchaseCreated event, given that you know an orderId to examine_

* @param orderId [uint256] the orderId to get details for
* @return [uint64] userId that this purchase is for
* @return [uint32] caseId that this purchase is made against
* @return [uint32] quantity of items purchased
* @return [uint256] block number that will seed the random selections

**CaseManager#getPurchaseResult(uint256 orderId, bytes32 blockHash) returns (uint32[], uint64[], uint16[], uint32, bytes32, bool)**

_Method. Gets the purchase results with item selections, knowing the correct blockhash.
  Note that the skus, wear values, and pattern indexes returned are array values.
  The values at index i correspond to the values for the i'th item purchased in this order.
  Will only return up to MAX_RESULT_PAGE_SIZE attributes. To get the remaining or page
  through the next set of results, call getMorePurchaseResult(uint256 orderId, uint256 startIndex, bytes32 nextSeed)
  Also, one should first check that the details for the orderId being queried looks as expected via
  the getOrderDetails method. You can confirm that the user, case, and quantity look right._

* @param orderId [uint256] the orderId to get results for
* @param blockHash [bytes32] the blockhash value to calculate results for
    Note: This blockhash provided should correspond to the hash at block
    blockNumber set on order orderId to be considered valid by definition.
    It is up to the caller to provide the correct blockhash!
    It is up to the caller to provide the correct blockhash as emitted in the PurchaseCreated
    event or available via the getOrderDetails method
* @return [uint32[]] skus for items selected from the case
* @return [uint64[]] wear values selected for the items
* @return [uint16[]] patternIndexes for the selected items
* @return [uint32] nextIndex next index to start at when more results are left to retrieve as indicated
    by the moreResults flag
* @return [bytes32] nextSeed next seed to use to retrieve the remaining results when the result set is
    larger than the MAX_RESULT_PAGE_SIZE. You will know this when moreResults is true
* @return [bool] moreResults flag indicating whether there are more results to get via getMorePurchaseResult

**CaseManager#getMorePurchaseResult(uint256 orderId, uint32 startIndex, bytes32 startSeed) returns (uint32[], uint64[], uint16[], uint32, bytes32, bool)**

_Method. Gets the purchase results with item selections, knowing the correct next seed and item index.
  Note that the skus, wear values, and pattern indexes returned are array values.
  The values at index i correspond to the values for the i'th item purchased in this order.
  Will only return up to MAX_RESULT_PAGE_SIZE attributes. To get the remaining or page
  through the next set of results, call getPurchaseResult(uint256 orderId, uint256 startIndex, bytes32 nextSeed)._

  * @param orderId [uint256] the orderId to get results for
  * @param startIndex [uint32] the next index to start at to get results for
  * @param startSeed [bytes32] the starting seed value to calculate results for
      Note: startSeed and startIndex should be the values provided by either a call to getPurchaseResult
      or getMorePurchaseResult. It is up to the caller to provide the correct next seed and item index as provided
      by one of these methods.
  * @return [uint32[]] skus for items selected from the case
  * @return [uint64[]] wear values selected for the items
  * @return [uint16[]] patternIndexes for the selected items
  * @return [uint32] nextIndex next index to start at when more results are left to retrieve as indicated
      by the moreResults flag
  * @return [bytes32] nextSeed next seed to use to retrieve the remaining results when the result set is
      larger than the MAX_RESULT_PAGE_SIZE. You will know this when moreResults is true
  * @return [bool] moreResults flag indicating whether there are more results to get via getMorePurchaseResult
