// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;
import "https://raw.githubusercontent.com/OpenZeppelin/openzeppelin-contracts/release-v4.8/contracts/token/ERC721/extensions/ERC721Enumerable.sol";

import "https://raw.githubusercontent.com/OpenZeppelin/openzeppelin-contracts/release-v4.8/contracts/access/Ownable.sol";
import "https://raw.githubusercontent.com/OpenZeppelin/openzeppelin-contracts/release-v4.8/contracts/utils/Strings.sol";
contract FatFUDkinBlunts is ERC721Enumerable, Ownable {

using Strings for uint256;
uint256 public constant MINT_PRICE = 4200000000000; // 0.0042 ETH in Wei


uint256 public constant MAX_MINT_PER_TRANSACTION = 10;
string private _baseTokenURI;

uint256 private _tokenIdCounter;
string[] private growOps = ["Indoor", "Outdoor", "Natural"];

string[] private types = ["Indica", "Sativa", "Hybrid"];
string[24] private tokenImages;
mapping(uint256 => string) public growOp;

mapping(uint256 => string) public strainType;
mapping(uint256 => uint256) public thcPercentage; // Mapping from token ID to THC percentage
mapping(uint256 => string) public tokenImageURLs; // Mapping from token ID to image URL
event Mint(

address indexed minter,
uint256 indexed tokenId,
uint256 indexed pricePaid,
uint256 thcContent
);
constructor(

string memory _name,
string memory _symbol,
string memory baseTokenURI
) ERC721(_name, _symbol) {
_baseTokenURI = baseTokenURI;
_tokenIdCounter = 1; // initializing the token ID counter
// Hardcoding placeholder images

tokenImages[0] = "https://github.com/JayRaTheRu/FatFUDkinBlunt/blob/c46607dd7cfede9ae2c33fdd74ef5a064314ce39/blunt1.png";
tokenImages[1] = "https://github.com/JayRaTheRu/FatFUDkinBlunt/blob/c46607dd7cfede9ae2c33fdd74ef5a064314ce39/blunt2.png";
tokenImages[2] = "https://github.com/JayRaTheRu/FatFUDkinBlunt/blob/c46607dd7cfede9ae2c33fdd74ef5a064314ce39/blunt3.png";
tokenImages[3] = "https://github.com/JayRaTheRu/FatFUDkinBlunt/blob/c46607dd7cfede9ae2c33fdd74ef5a064314ce39/blunt4.png";
tokenImages[4] = "https://github.com/JayRaTheRu/FatFUDkinBlunt/blob/c46607dd7cfede9ae2c33fdd74ef5a064314ce39/blunt5.png";
tokenImages[5] = "https://github.com/JayRaTheRu/FatFUDkinBlunt/blob/c46607dd7cfede9ae2c33fdd74ef5a064314ce39/blunt6.png";
tokenImages[6] = "https://github.com/JayRaTheRu/FatFUDkinBlunt/blob/c46607dd7cfede9ae2c33fdd74ef5a064314ce39/blunt7.png";
tokenImages[7] = "https://github.com/JayRaTheRu/FatFUDkinBlunt/blob/c46607dd7cfede9ae2c33fdd74ef5a064314ce39/blunt8.png";
tokenImages[8] = "https://github.com/JayRaTheRu/FatFUDkinBlunt/blob/c46607dd7cfede9ae2c33fdd74ef5a064314ce39/blunt9.png";
tokenImages[9] = "https://github.com/JayRaTheRu/FatFUDkinBlunt/blob/c46607dd7cfede9ae2c33fdd74ef5a064314ce39/blunt10.png";
tokenImages[10] = "https://github.com/JayRaTheRu/FatFUDkinBlunt/blob/c46607dd7cfede9ae2c33fdd74ef5a064314ce39/blunt11.png";
tokenImages[11] = "https://github.com/JayRaTheRu/FatFUDkinBlunt/blob/c46607dd7cfede9ae2c33fdd74ef5a064314ce39/blunt12.png";
tokenImages[12] = "https://github.com/JayRaTheRu/FatFUDkinBlunt/blob/c46607dd7cfede9ae2c33fdd74ef5a064314ce39/blunt13.png";
tokenImages[13] = "https://github.com/JayRaTheRu/FatFUDkinBlunt/blob/c46607dd7cfede9ae2c33fdd74ef5a064314ce39/blunt14.png";
tokenImages[14] = "https://github.com/JayRaTheRu/FatFUDkinBlunt/blob/c46607dd7cfede9ae2c33fdd74ef5a064314ce39/blunt15wax.png";
tokenImages[15] = "https://github.com/JayRaTheRu/FatFUDkinBlunt/blob/c46607dd7cfede9ae2c33fdd74ef5a064314ce39/blunt16wax.png";
tokenImages[16] = "https://github.com/JayRaTheRu/FatFUDkinBlunt/blob/c46607dd7cfede9ae2c33fdd74ef5a064314ce39/blunt17wax.png";
tokenImages[17] = "https://github.com/JayRaTheRu/FatFUDkinBlunt/blob/c46607dd7cfede9ae2c33fdd74ef5a064314ce39/blunt18wax.png";
tokenImages[18] = "https://github.com/JayRaTheRu/FatFUDkinBlunt/blob/c46607dd7cfede9ae2c33fdd74ef5a064314ce39/blunt19wax.png";
tokenImages[19] = "https://github.com/JayRaTheRu/FatFUDkinBlunt/blob/c46607dd7cfede9ae2c33fdd74ef5a064314ce39/blunt20wax.png";
tokenImages[20] = "https://github.com/JayRaTheRu/FatFUDkinBlunt/blob/c46607dd7cfede9ae2c33fdd74ef5a064314ce39/blunt21wax.png";
tokenImages[21] = "https://github.com/JayRaTheRu/FatFUDkinBlunt/blob/c46607dd7cfede9ae2c33fdd74ef5a064314ce39/blunt22wax.png";
tokenImages[22] = "https://github.com/JayRaTheRu/FatFUDkinBlunt/blob/c46607dd7cfede9ae2c33fdd74ef5a064314ce39/blunt23wax.png";
tokenImages[23] = "https://github.com/JayRaTheRu/FatFUDkinBlunt/blob/c46607dd7cfede9ae2c33fdd74ef5a064314ce39/blunt24mega.png";
}
function mint(uint256 numberOfTokens) external payable {

require(
numberOfTokens > 0 && numberOfTokens <= MAX_MINT_PER_TRANSACTION,
"Invalid number of tokens"
);
require(
msg.value == MINT_PRICE * numberOfTokens,
"Insufficient ETH sent"
);
for (uint256 i = 0; i < numberOfTokens; i++) {

uint256 newItemId = _tokenIdCounter;
_safeMint(msg.sender, newItemId);
// Randomly assign grow op, strain type, and image URL

growOp[newItemId] = growOps[random(0, growOps.length)];
strainType[newItemId] = types[random(0, types.length)];
tokenImageURLs[newItemId] = tokenImages[random(0, 24)];
// Assign THC percentage based on rarity

thcPercentage[newItemId] = generateThcPercentage();
emit Mint(msg.sender, newItemId, MINT_PRICE, thcPercentage[newItemId]);

// Increment the token ID counter after minting

_tokenIdCounter++;
}
}
function generateThcPercentage() internal view returns (uint256) {

uint256 rareRoll = random(1, 1000);
if (rareRoll == 1) {
return 100; // Super rare 100% THC
} else {
uint256 lowThcRoll = random(1, 100);
if (lowThcRoll <= 10) { // 10% chance for low THC
return random(0, 79); // THC between 0% and 79%
} else {
return random(85, 95); // Common THC range between 85% and 95%
}
}
}
function setBaseURI(string memory baseURI) external onlyOwner {

_baseTokenURI = baseURI;
}
function _baseURI() internal view override returns (string memory) {

return _baseTokenURI;
}
function tokenURI(uint256 tokenId)

public
view
override
returns (string memory)
{
require(
_exists(tokenId),
"ERC721Metadata: URI query for nonexistent token"
);
string memory baseURI = _baseURI();

return
bytes(baseURI).length > 0
? string(abi.encodePacked(baseURI, tokenId.toString(), tokenImageURLs[tokenId]))
: "";
}
function withdraw() external onlyOwner {

payable(owner()).transfer(address(this).balance);
}
// Function to generate a pseudo-random number between a range

function random(uint256 from, uint256 to) internal view returns (uint256) {
uint256 randomNumber = uint256(
keccak256(
abi.encodePacked(
block.timestamp,
block.prevrandao, // Updated to use prevrandao
_tokenIdCounter
)
)
);
return (randomNumber % (to - from)) + from;
}
}
