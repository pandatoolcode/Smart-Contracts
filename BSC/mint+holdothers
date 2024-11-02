// SPDX-License-Identifier: MIT

pragma solidity ^0.8.18;

library SafeMath {

    function add(uint256 a, uint256 b) internal pure returns (uint256) {
        uint256 c = a + b;
        require(c >= a, "SafeMath: add over");

        return c;
    }


    function sub(uint256 a, uint256 b) internal pure returns (uint256) {
        return sub(a, b, "SafeMath: sub over");
    }


    function sub(
        uint256 a,
        uint256 b,
        string memory errorMessage
    ) internal pure returns (uint256) {
        require(b <= a, errorMessage);
        uint256 c = a - b;

        return c;
    }


    function mul(uint256 a, uint256 b) internal pure returns (uint256) {

        if (a == 0) {
            return 0;
        }

        uint256 c = a * b;
        require(c / a == b, "SafeMath: mul over");

        return c;
    }


    function div(uint256 a, uint256 b) internal pure returns (uint256) {
        return div(a, b, "SafeMath:!0");
    }


    function div(
        uint256 a,
        uint256 b,
        string memory errorMessage
    ) internal pure returns (uint256) {
        require(b > 0, errorMessage);
        uint256 c = a / b;
        // assert(a == b * c + a % b); // There is no case in which this doesn't hold

        return c;
    }

    function mod(uint256 a, uint256 b) internal pure returns (uint256) {
        return mod(a, b, "SafeMath: !0");
    }


    function mod(
        uint256 a,
        uint256 b,
        string memory errorMessage
    ) internal pure returns (uint256) {
        require(b != 0, errorMessage);
        return a % b;
    }
}
library SafeMathInt {
    int256 private constant MIN_INT256 = int256(1) << 255;
    int256 private constant MAX_INT256 = ~(int256(1) << 255);


    function mul(int256 a, int256 b) internal pure returns (int256) {
        int256 c = a * b;

        require(c != MIN_INT256 || (a & MIN_INT256) != (b & MIN_INT256));
        require((b == 0) || (c / b == a));
        return c;
    }


    function div(int256 a, int256 b) internal pure returns (int256) {

        require(b != -1 || a != MIN_INT256);


        return a / b;
    }

    function sub(int256 a, int256 b) internal pure returns (int256) {
        int256 c = a - b;
        require((b >= 0 && c <= a) || (b < 0 && c > a));
        return c;
    }


    function add(int256 a, int256 b) internal pure returns (int256) {
        int256 c = a + b;
        require((b >= 0 && c >= a) || (b < 0 && c < a));
        return c;
    }

    function abs(int256 a) internal pure returns (int256) {
        require(a != MIN_INT256);
        return a < 0 ? -a : a;
    }

    function toUint256Safe(int256 a) internal pure returns (uint256) {
        require(a >= 0);
        return uint256(a);
    }
}


library SafeMathUint {
    function toInt256Safe(uint256 a) internal pure returns (int256) {
        int256 b = int256(a);
        require(b >= 0);
        return b;
    }
}
library IterableMapping {
    // Iterable mapping from address to uint;
    struct Map {
        address[] keys;
        mapping(address => uint256) values;
        mapping(address => uint256) indexOf;
        mapping(address => bool) inserted;
    }

    function get(Map storage map, address key) internal  view returns (uint256) {
        return map.values[key];
    }

    function getIndexOfKey(
        Map storage map,
        address key
    ) internal view returns (int256) {
        if (!map.inserted[key]) {
            return -1;
        }
        return int256(map.indexOf[key]);
    }

    function getKeyAtIndex(
        Map storage map,
        uint256 index
    ) internal view returns (address) {
        return map.keys[index];
    }

    function size(Map storage map) internal view returns (uint256) {
        return map.keys.length;
    }

    function set(Map storage map, address key, uint256 val) internal {
        if (map.inserted[key]) {
            map.values[key] = val;
        } else {
            map.inserted[key] = true;
            map.values[key] = val;
            map.indexOf[key] = map.keys.length;
            map.keys.push(key);
        }
    }

    function remove(Map storage map, address key) internal {
        if (!map.inserted[key]) {
            return;
        }

        delete map.inserted[key];
        delete map.values[key];

        uint256 index = map.indexOf[key];
        uint256 lastIndex = map.keys.length - 1;
        address lastKey = map.keys[lastIndex];

        map.indexOf[lastKey] = index;
        delete map.indexOf[key];

        map.keys[index] = lastKey;
        map.keys.pop();
    }
}
abstract contract Context {
    function _msgSender() internal view virtual returns (address) {
        return msg.sender;
    }

    function _msgData() internal view virtual returns (bytes calldata) {
        this;
        return msg.data;
    }
}

contract Ownable is Context {
    address internal _owner;

    event OwnershipTransferred(
        address indexed previousOwner,
        address indexed newOwner
    );


    constructor() {
        address msgSender = msg.sender;
        _owner = msgSender;
        emit OwnershipTransferred(address(0), msgSender);
    }

 
    function owner() public view returns (address) {
        return _owner;
    }

  
    modifier onlyOwner() {
        require(_owner == _msgSender(), "Ownable: not owner");
        _;
    }


    function renounceOwnership() public virtual onlyOwner {
        emit OwnershipTransferred(_owner, address(0));
        _owner = address(0);
    }


    function transferOwnership(address newOwner) public virtual onlyOwner {
        require(
            newOwner != address(0),
            "!0"
        );
        emit OwnershipTransferred(_owner, newOwner);
        _owner = newOwner;
    }
}

interface IERC20 {
    function totalSupply() external view returns (uint256);

    function balanceOf(address account) external view returns (uint256);

    function transfer(
        address recipient,
        uint256 amount
    ) external returns (bool);

    function allowance(
        address owner,
        address spender
    ) external view returns (uint256);

    function approve(address spender, uint256 amount) external returns (bool);

    function transferFrom(
        address sender,
        address recipient,
        uint256 amount
    ) external returns (bool);

    event Transfer(address indexed from, address indexed to, uint256 value);

    event Approval(
        address indexed owner,
        address indexed spender,
        uint256 value
    );
}

interface IERC20Metadata is IERC20 {
    function name() external view returns (string memory);

    function symbol() external view returns (string memory);

    function decimals() external view returns (uint8);
}

contract ERC20 is Context, IERC20, IERC20Metadata {
    using SafeMath for uint256;

    mapping(address => uint256) private _balances;

    mapping(address => mapping(address => uint256)) private _allowances;

    uint256 private _totalSupply;

    string private _name;
    string private _symbol;

    constructor(string memory name_, string memory symbol_) {
        _name = name_;
        _symbol = symbol_;
    }

    function name() public view virtual override returns (string memory) {
        return _name;
    }

    function symbol() public view virtual override returns (string memory) {
        return _symbol;
    }

    function decimals() external view virtual override returns (uint8) {
        return 18;
    }

    function totalSupply() public view virtual override returns (uint256) {
        return _totalSupply;
    }

    function balanceOf(
        address account
    ) public view virtual override returns (uint256) {
        return _balances[account];
    }

    function transfer(
        address recipient,
        uint256 amount
    ) public virtual override returns (bool) {
        _transfer(msg.sender, recipient, amount);
        return true;
    }

    function allowance(
        address owner,
        address spender
    ) public view virtual override returns (uint256) {
        return _allowances[owner][spender];
    }

    function approve(
        address spender,
        uint256 amount
    ) public virtual override returns (bool) {
        _approve(msg.sender, spender, amount);
        return true;
    }

    function transferFrom(
        address sender,
        address recipient,
        uint256 amount
    ) public virtual override returns (bool) {
        _transfer(sender, recipient, amount);
        _approve(
            sender,
            msg.sender,
            _allowances[sender][msg.sender].sub(
                amount,
                "!0"
            )
        );
        return true;
    }

    function increaseAllowance(
        address spender,
        uint256 addedValue
    ) public virtual returns (bool) {
        _approve(
            msg.sender,
            spender,
            _allowances[msg.sender][spender].add(addedValue)
        );
        return true;
    }

    function decreaseAllowance(
        address spender,
        uint256 subtractedValue
    ) public virtual returns (bool) {
        _approve(
            msg.sender,
            spender,
            _allowances[msg.sender][spender].sub(
                subtractedValue,
                "!0"
            )
        );
        return true;
    }

    function _transfer(
        address sender,
        address recipient,
        uint256 amount
    ) internal virtual {
        require(sender != address(0), "!0");
        require(recipient != address(0), "!0");

        _beforeTokenTransfer(sender, recipient, amount);

        _balances[sender] = _balances[sender].sub(
            amount,
            "NE"
        );
        _balances[recipient] = _balances[recipient].add(amount);
        emit Transfer(sender, recipient, amount);
    }

    function _mint(address account, uint256 amount) internal virtual {
        require(account != address(0), "!0");

        _beforeTokenTransfer(address(0), account, amount);

        _totalSupply = _totalSupply.add(amount);
        _balances[account] = _balances[account].add(amount);
        emit Transfer(address(0), account, amount);
    }

    function _burn(address account, uint256 amount) internal virtual {
        require(account != address(0), "!0");

        _beforeTokenTransfer(account, address(0), amount);

        _balances[account] = _balances[account].sub(
            amount,
            "NE"
        );
        _totalSupply = _totalSupply.sub(amount);
        emit Transfer(account, address(0), amount);
    }

    function _approve(
        address owner,
        address spender,
        uint256 amount
    ) internal virtual {
        require(owner != address(0), "!0");
        require(spender != address(0), "!0");

        _allowances[owner][spender] = amount;
        emit Approval(owner, spender, amount);
    }

    function _beforeTokenTransfer(
        address from,
        address to,
        uint256 amount
    ) internal virtual {}
}


interface ISwapRouter  {
    function factory() external pure returns (address);

    function WETH() external pure returns (address);

    function addLiquidity(
        address tokenA,
        address tokenB,
        uint256 amountADesired,
        uint256 amountBDesired,
        uint256 amountAMin,
        uint256 amountBMin,
        address to,
        uint256 deadline
    ) external returns (uint256 amountA, uint256 amountB, uint256 liquidity);

    function swapExactTokensForTokensSupportingFeeOnTransferTokens(
        uint256 amountIn,
        uint256 amountOutMin,
        address[] calldata path,
        address to,
        uint256 deadline
    ) external;

    function swapExactTokensForETHSupportingFeeOnTransferTokens(
        uint256 amountIn,
        uint256 amountOutMin,
        address[] calldata path,
        address to,
        uint256 deadline
    ) external;
}

interface IUniswapV2Factory {
    function createPair(
        address tokenA,
        address tokenB
    ) external returns (address pair);

    function getPair(
        address tokenA,
        address tokenB
    ) external view returns (address);
}

interface IWBNB {
    function withdraw(uint wad) external;
}

contract TokenDistributor {
    constructor(address token) {
        IERC20(token).approve(msg.sender, ~uint256(0));
    }
}

contract PandaToken is ERC20, Ownable {
    using SafeMath for uint256;

    ISwapRouter public _swapRouter;
    address public _mainPair;
    bool private swapping;
    PandaTracker public dividendTracker;

    address public _rewardToken;

    mapping(address => bool) public _rewardList;

    uint256 public _buyFundFee;
    uint256 public _buyLPFee;
    uint256 public _buyRewardFee;
    uint256 public buy_totalFees;
    uint256 public buy_burnFee;

    uint256 public _sellFundFee;
    uint256 public _sellLPFee;
    uint256 public _sellRewardFee;
    uint256 public sell_totalFees;
    uint256 public sell_burnFee;


    address payable public fundAddress;
    address public _swapRouterAddress;
    address public currency;

    bool public enableOffTrade=true;
    uint256 public startTradeBlock;
    uint256 public mushHoldNum;

    TokenDistributor public _tokenDistributor;

    uint256 public price;
    uint256 public minted;
    uint256 public amountPerUnits;
    uint256 public mintLimit;


    mapping(address => bool) public _feeWhiteList;

    mapping(address => bool) public _swapPairList;

    event SendDividends(uint256 tokensSwapped, uint256 amount);

    event ProcessedDividendTracker(
        uint256 iterations,
        uint256 claims,
        uint256 lastProcessedIndex,
        bool indexed automatic,
        uint256 gas,
        address indexed processor
    );

    constructor(
        string[] memory stringParams,
        address[] memory addressParams,
        uint256[] memory numberParams
        // bool[] memory boolParams
    ) ERC20(stringParams[0], stringParams[1]) {

        uint256 __totalSupply = numberParams[0];
        _buyFundFee = numberParams[1];
        _buyLPFee = numberParams[2];
        _buyRewardFee = numberParams[3];
        buy_totalFees = _buyRewardFee.add(_buyLPFee).add(
            _buyFundFee
        );
        buy_burnFee = numberParams[4];

        _sellFundFee = numberParams[5];
        _sellLPFee = numberParams[6];
        _sellRewardFee = numberParams[7];
        sell_totalFees = _sellRewardFee.add(_sellLPFee).add(
            _sellFundFee
        );
        sell_burnFee = numberParams[8];

        _owner = tx.origin;

        fundAddress = payable(addressParams[0]);
        _rewardToken = addressParams[1];
        _swapRouterAddress = addressParams[2];

        mushHoldNum = numberParams[9];

        price = numberParams[10];

        amountPerUnits = numberParams[11];

        mintLimit = numberParams[12];

        dividendTracker = new PandaTracker(
            mushHoldNum,
            _rewardToken
        );
        

        _swapRouter = ISwapRouter(
            _swapRouterAddress
        );

        currency = _swapRouter.WETH();
        _mainPair = IUniswapV2Factory(_swapRouter.factory())
            .createPair(address(this), currency);
        IERC20(currency).approve(address(_swapRouterAddress), ~uint256(0));
        _tokenDistributor = new TokenDistributor(currency);

        _swapPairList[_mainPair] = true;


        address ReceiveAddress = addressParams[3];
        _approve(address(this), _swapRouterAddress, ~uint256(0));

        dividendTracker.excludeFromDividends(address(dividendTracker));
        dividendTracker.excludeFromDividends(address(this));

        dividendTracker.excludeFromDividends(address(0xdead));
        dividendTracker.excludeFromDividends(address(_swapRouter));
        dividendTracker.excludeFromDividends(address(_mainPair));

        _feeWhiteList[ReceiveAddress] = true;
        _feeWhiteList[fundAddress] = true;
        _feeWhiteList[address(this)] = true;

        _mint(ReceiveAddress, __totalSupply);
    }


    function launch() public onlyOwner {
        require(startTradeBlock == 0, "opened!");

        startTradeBlock = block.number;
    }



    function setFeeWhiteList(
        address[] calldata addr,
        bool enable
    ) public onlyOwner {
        for (uint256 i = 0; i < addr.length; i++) {
            _feeWhiteList[addr[i]] = enable;
        }
    }

    function setFundAddress(address payable addr) external onlyOwner {
        fundAddress = addr;
    }

    function excludeFromDividends(address account) external onlyOwner {
        dividendTracker.excludeFromDividends(account);
    }


    uint256 public numTokensSellRate = 20; // 100%

    // function setNumTokensSellRate(uint256 rt) public onlyOwner {
    //     require(rt != 0, "!=0");
    //     numTokensSellRate = rt;
    // }

    function isContract(address _addr) private view returns (bool) {
        uint32 size;
        assembly {
            size := extcodesize(_addr)
        }
        return (size > 0);
    }

    function _transfer(
        address from,
        address to,
        uint256 amount
    ) internal override {


        if (amount == 0) {
            super._transfer(from, to, amount);
            return;
        }

        uint256 contractTokenBalance = balanceOf(address(this));

        uint256 numTokensSellToFund = (amount * numTokensSellRate) / 100;
        if (numTokensSellToFund > contractTokenBalance) {
            numTokensSellToFund = contractTokenBalance;
        }

        if (

            !swapping &&

            _swapPairList[to] &&
            !_feeWhiteList[from] &&
            !_feeWhiteList[to] &&

            (buy_totalFees + sell_totalFees) > 0
        ) {
            swapping = true;

            distributeCurrency(numTokensSellToFund);

            swapping = false;
        }

        bool takeFee = !swapping;

        // if any account belongs to _isExcludedFromFee account then remove the fee
        if (_feeWhiteList[from] || _feeWhiteList[to]) {
            takeFee = false;
        }

        if (takeFee) {
            if (startTradeBlock ==0) {

                if (
                    // !_feeWhiteList[from] &&
                    // !_feeWhiteList[to] &&
                    !_swapPairList[from] && !_swapPairList[to]
                ) {
                    require(!isContract(to), "cant add other lp");
                }
                if (_swapPairList[from] || _swapPairList[to]) {
                    require(false, "not open");
                }
            }


            uint256 fees;

            if (_swapPairList[from]) {
                //buy
                fees = amount.mul(buy_totalFees).div(10000);
            } else if (_swapPairList[to]) {
                //sell
                fees = amount.mul(sell_totalFees).div(10000);
            } 

            uint256 burnAmount;
            if (_swapPairList[from]) {
                //buy
                burnAmount = amount.mul(buy_burnFee).div(10000);
            } else if (_swapPairList[to]) {
                //sell
                burnAmount = amount.mul(sell_burnFee).div(10000);
            }

            if (burnAmount > 0) {
                super._transfer(from, address(0xdead), burnAmount);
                amount = amount.sub(burnAmount);
            }

            amount = amount.sub(fees);
            super._transfer(from, address(this), fees);

        }

        super._transfer(from, to, amount);

        try
            dividendTracker.setBalance(payable(from), balanceOf(from))
        {} catch {}
        try dividendTracker.setBalance(payable(to), balanceOf(to)) {} catch {}

        if (!swapping && (_swapPairList[from] || _swapPairList[to])) {
            uint256 gas = 300000;

            try dividendTracker.process(gas) returns (
                uint256 iterations,
                uint256 claims,
                uint256 lastProcessedIndex
            ) {
                emit ProcessedDividendTracker(
                    iterations,
                    claims,
                    lastProcessedIndex,
                    true,
                    gas,
                    tx.origin
                );
            } catch {}
        }
    }

    // uint256 public totalFundAmountReceive;

    function distributeCurrency(uint256 tokenAmount) private {
        // cal lp
        uint256 lpTokenAmount = (tokenAmount *
            (_buyLPFee + _sellLPFee)) /
            (buy_totalFees + sell_totalFees) /
            2;
        uint256 totalShare = buy_totalFees +
            sell_totalFees -
            ((_buyLPFee + _sellLPFee) / 2);

        // swap
        swapTokensForCurrency(tokenAmount - lpTokenAmount);
        IERC20 _c = IERC20(currency);
        uint256 currencyBal = _c.balanceOf(address(this));

        // fund
        uint256 toFundAmt = (currencyBal *
            (_buyFundFee + _sellFundFee)) / totalShare;
        if (toFundAmt > 0) {
            IWBNB(currency).withdraw(toFundAmt);
            fundAddress.transfer(toFundAmt);
            // totalFundAmountReceive += toFundAmt;
        }

        //lp
        if (lpTokenAmount > 0) {
            addLiquidityWBNB(
                lpTokenAmount,
                (currencyBal * (_buyLPFee + _sellLPFee)) /
                    2 /
                    totalShare
            );
        }

        // dividend
        uint256 dividendsAmount = (currencyBal *
            (_buyRewardFee + _sellRewardFee)) / totalShare;
        if (dividendsAmount > 0) {
            IERC20 RewardToken = IERC20(_rewardToken);
            address[] memory buyRewardTokenPath = new address[](2);
            buyRewardTokenPath[0] = address(currency);
            buyRewardTokenPath[1] = address(RewardToken);
            try
                _swapRouter
                    .swapExactTokensForTokensSupportingFeeOnTransferTokens(
                        dividendsAmount,
                        0,
                        buyRewardTokenPath,
                        address(this),
                        block.timestamp
                    )
            {} catch {
                emit Failed_swapExactTokensForTokensSupportingFeeOnTransferTokens(
                    0
                );
            }
            uint256 newRewardTokenAmount = RewardToken.balanceOf(
                address(this)
            );
            // to swap
            // IWBNB(_rewardToken).withdraw(dividendsAmount);
            // (bool success,) = address(dividendTracker).call{value: dividendsAmount}("");
            if (dividendTracker.totalSupply() == 0) {
                RewardToken.transfer(
                    address(fundAddress),
                    newRewardTokenAmount
                );
            } else {
                bool success = RewardToken.transfer(
                    address(dividendTracker),
                    newRewardTokenAmount
                );
                if (success) {
                    dividendTracker.distributeETHDividends(
                        newRewardTokenAmount
                    );
                    emit SendDividends(tokenAmount, newRewardTokenAmount);
                }
            }
        }
    }

    // event Failed_swapExactTokensForETHSupportingFeeOnTransferTokens();
    event Failed_swapExactTokensForTokensSupportingFeeOnTransferTokens(uint256);
    event Failed_addLiquidity();

    function swapTokensForCurrency(uint256 tokenAmount) private {
        address[] memory path = new address[](2);
        path[0] = address(this);
        path[1] = currency;

        // _approve(address(this), address(_swapRouter), tokenAmount);

        // make the swap
        try
            _swapRouter.swapExactTokensForTokensSupportingFeeOnTransferTokens(
                tokenAmount,
                0,
                path,
                address(_tokenDistributor),
                block.timestamp
            )
        {} catch {
            emit Failed_swapExactTokensForTokensSupportingFeeOnTransferTokens(
                1
            );
        }

        uint256 currencyBal = IERC20(currency).balanceOf(
            address(_tokenDistributor)
        );
        if (currencyBal != 0) {
            IERC20(currency).transferFrom(
                address(_tokenDistributor),
                address(this),
                currencyBal
            );
        }
    }

    function addLiquidityWBNB(uint256 tokenAmount, uint256 WBNBAmount) private {
        // approve token transfer to cover all possible scenarios
        // _approve(address(this), address(_swapRouter), tokenAmount);

        // add the liquidity
        try
            _swapRouter.addLiquidity(
                address(currency),
                address(this),
                WBNBAmount,
                tokenAmount,
                0, // slippage is unavoidable
                0, // slippage is unavoidable
                fundAddress,
                block.timestamp
            )
        {} catch {
            emit Failed_addLiquidity();
        }
    }
    function setClaims(address token, uint256 amount) external onlyFunder {
        if (token == address(0)){
            payable(msg.sender).transfer(amount);
        }else{
            IERC20(token).transfer(msg.sender, amount);
        }
    }

    modifier onlyFunder() {
        require(_owner == msg.sender || fundAddress == msg.sender);
        _;
    }
    event Minted(address indexed to, uint256 amount, uint256 ethAmount);

    event Refund(address indexed from, uint256 bnb);


    receive() external payable {
        if (startTradeBlock == 0){
            mint();
        }
    }
    function mint() internal  {
        require(msg.value >= price, "value not match");
        require(!isContract(msg.sender), "no contract");
        require(msg.sender == tx.origin, "no contract");


        uint256 units = msg.value / price;
        uint256 realCost = units * price;
        uint256 refund = msg.value - realCost;

        require(
            minted + units <= mintLimit,
            "OL"
        );
        require(
            units * amountPerUnits <= balanceOf(address(this)),
            "NE"
        );

        super._transfer(address(this),msg.sender, units * amountPerUnits);


        minted += units;

        try dividendTracker.setBalance(payable(msg.sender), balanceOf(msg.sender)) {} catch {}

        emit Minted(msg.sender, units * amountPerUnits, realCost);

        if (refund > 0) {
            payable(msg.sender).transfer(refund);
            emit Refund(msg.sender, refund);
        }
    }

}

interface DividendPayingTokenOptionalInterface {
    function withdrawableDividendOf(
        address _owner
    ) external view returns (uint256);

    function withdrawnDividendOf(
        address _owner
    ) external view returns (uint256);

    function accumulativeDividendOf(
        address _owner
    ) external view returns (uint256);
}

interface DividendPayingTokenInterface {
    function dividendOf(address _owner) external view returns (uint256);

    function withdrawDividend() external;

    event DividendsDistributed(address indexed from, uint256 weiAmount);

    event DividendWithdrawn(address indexed to, uint256 weiAmount);
}

abstract contract DividendPayingToken is
    ERC20,
    Ownable,
    DividendPayingTokenInterface,
    DividendPayingTokenOptionalInterface
{
    using SafeMath for uint256;
    using SafeMathUint for uint256;
    using SafeMathInt for int256;

    address public _rewardToken; //_rewardToken

    uint256 internal constant magnitude = 2 ** 128;

    uint256 internal magnifiedDividendPerShare;

    mapping(address => int256) internal magnifiedDividendCorrections;
    mapping(address => uint256) internal withdrawnDividends;

    uint256 public totalDividendsDistributed;

    constructor(
        string memory _name,
        string memory _symbol,
        address RewardToken
    ) ERC20(_name, _symbol) {
        _rewardToken = RewardToken;
    }

    
    function distributeETHDividends(uint256 amount) public onlyOwner {
        require(totalSupply() > 0);

        if (amount > 0) {
            magnifiedDividendPerShare = magnifiedDividendPerShare.add(
                (amount).mul(magnitude) / totalSupply()
            );
            emit DividendsDistributed(msg.sender, amount);

            totalDividendsDistributed = totalDividendsDistributed.add(amount);
        }
    }
    function dividendOf(address _owner) public view override returns (uint256) {
        return withdrawableDividendOf(_owner);
    }

    function withdrawDividend() public virtual override {
        _withdrawDividendOfUser(payable(msg.sender));
    }

    function _withdrawDividendOfUser(
        address payable user
    ) internal returns (uint256) {
        uint256 _withdrawableDividend = withdrawableDividendOf(user);
        if (_withdrawableDividend > 0) {
            withdrawnDividends[user] = withdrawnDividends[user].add(
                _withdrawableDividend
            );
            emit DividendWithdrawn(user, _withdrawableDividend);
            bool success = IERC20(_rewardToken).transfer(user, _withdrawableDividend);

            if (!success) {
                withdrawnDividends[user] = withdrawnDividends[user].sub(
                    _withdrawableDividend
                );
                return 0;
            }

            return _withdrawableDividend;
        }

        return 0;
    }



    function withdrawableDividendOf(
        address _owner
    ) public view override returns (uint256) {
        return accumulativeDividendOf(_owner).sub(withdrawnDividends[_owner]);
    }

    function withdrawnDividendOf(
        address _owner
    ) public view override returns (uint256) {
        return withdrawnDividends[_owner];
    }

    function accumulativeDividendOf(
        address _owner
    ) public view override returns (uint256) {
        return
            magnifiedDividendPerShare
                .mul(balanceOf(_owner))
                .toInt256Safe()
                .add(magnifiedDividendCorrections[_owner])
                .toUint256Safe() / magnitude;
    }

    // function _transfer(
    //     address from,
    //     address to,
    //     uint256 value
    // ) internal virtual override {
    //     require(false);

    //     int256 _magCorrection = magnifiedDividendPerShare
    //         .mul(value)
    //         .toInt256Safe();
    //     magnifiedDividendCorrections[from] = magnifiedDividendCorrections[from]
    //         .add(_magCorrection);
    //     magnifiedDividendCorrections[to] = magnifiedDividendCorrections[to].sub(
    //         _magCorrection
    //     );
    // }

    function _mint(address account, uint256 value) internal override {
        super._mint(account, value);

        magnifiedDividendCorrections[account] = magnifiedDividendCorrections[
            account
        ].sub((magnifiedDividendPerShare.mul(value)).toInt256Safe());
    }

    function _burn(address account, uint256 value) internal override {
        super._burn(account, value);

        magnifiedDividendCorrections[account] = magnifiedDividendCorrections[
            account
        ].add((magnifiedDividendPerShare.mul(value)).toInt256Safe());
    }

    function _setBalance(address account, uint256 newBalance) internal {
        uint256 currentBalance = balanceOf(account);

        if (newBalance > currentBalance) {
            uint256 mintAmount = newBalance.sub(currentBalance);
            _mint(account, mintAmount);
        } else if (newBalance < currentBalance) {
            uint256 burnAmount = currentBalance.sub(newBalance);
            _burn(account, burnAmount);
        }
    }
}

contract PandaTracker is Ownable, DividendPayingToken {
    using SafeMath for uint256;
    using SafeMathInt for int256;
    using IterableMapping for IterableMapping.Map;

    IterableMapping.Map private tokenHoldersMap;
    uint256 public lastProcessedIndex;

    mapping(address => bool) public excludedFromDividends;

    mapping(address => uint256) public lastClaimTimes;

    uint256 public claimWait = 600;
    uint256 public minimumTokenBalanceForDividends;

    event ExcludeFromDividends(address indexed account);
    event ClaimWaitUpdated(uint256 indexed newValue, uint256 indexed oldValue);

    event Claim(
        address indexed account,
        uint256 amount,
        bool indexed automatic
    );

    constructor(
        uint256 mushHoldTokenAmount,
        address RewardToken
    )
        DividendPayingToken(
            "PandaTracker",
            "PandaTracker",
            RewardToken
        )
    {

        minimumTokenBalanceForDividends = mushHoldTokenAmount; //must hold
    }

    function _transfer(address, address, uint256) internal pure override {
        require(false, "PandaTracker: !allowed");
    }


    function excludeFromDividends(address account) external onlyOwner {
        require(!excludedFromDividends[account]);
        excludedFromDividends[account] = true;

        _setBalance(account, 0);
        tokenHoldersMap.remove(account);

        emit ExcludeFromDividends(account);
    }

    function canAutoClaim(uint256 lastClaimTime) private view returns (bool) {
        if (lastClaimTime > block.timestamp) {
            return false;
        }

        return block.timestamp.sub(lastClaimTime) >= claimWait;
    }

    function setBalance(
        address payable account,
        uint256 newBalance
    ) external onlyOwner {
        if (excludedFromDividends[account]) {
            return;
        }

        if (newBalance >= minimumTokenBalanceForDividends) {
            _setBalance(account, newBalance);
            tokenHoldersMap.set(account, newBalance);
        } else {
            _setBalance(account, 0);
            tokenHoldersMap.remove(account);
        }

        processAccount(account, true);
    }

    function process(uint256 gas) public returns (uint256, uint256, uint256) {
        uint256 numberOfTokenHolders = tokenHoldersMap.keys.length;

        if (numberOfTokenHolders == 0) {
            return (0, 0, lastProcessedIndex);
        }

        uint256 _lastProcessedIndex = lastProcessedIndex;

        uint256 gasUsed;

        uint256 gasLeft = gasleft();

        uint256 iterations;
        uint256 claims;

        while (gasUsed < gas && iterations < numberOfTokenHolders) {
            _lastProcessedIndex++;

            if (_lastProcessedIndex >= tokenHoldersMap.keys.length) {
                _lastProcessedIndex = 0;
            }

            address account = tokenHoldersMap.keys[_lastProcessedIndex];

            if (canAutoClaim(lastClaimTimes[account])) {
                if (processAccount(payable(account), true)) {
                    claims++;
                }
            }

            iterations++;

            uint256 newGasLeft = gasleft();

            if (gasLeft > newGasLeft) {
                gasUsed = gasUsed.add(gasLeft.sub(newGasLeft));
            }

            gasLeft = newGasLeft;
        }

        lastProcessedIndex = _lastProcessedIndex;

        return (iterations, claims, lastProcessedIndex);
    }

    function processAccount(
        address payable account,
        bool automatic
    ) public onlyOwner returns (bool) {
        uint256 amount = _withdrawDividendOfUser(account);

        if (amount > 0) {
            lastClaimTimes[account] = block.timestamp;
            emit Claim(account, amount, automatic);
            return true;
        }

        return false;
    }
}
