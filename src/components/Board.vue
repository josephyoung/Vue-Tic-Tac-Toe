<script>
import Square from './Square'

export default ({ props }) => {
  const renderSquare = (i, squareStyle) => {
    const value = props.squares[i];
    if(squareStyle) {
      return (<Square
                value={ value }
                handleClick={ () => props.handleClick(i) }
                key={ i }
                squareStyle={ squareStyle }
              />);
    } else {
      return (<Square
                value={ value }
                handleClick={ () => props.handleClick(i) }
                key={ i }
              />);
    }
  }

  let element = [];
  for (let i = 0; i < 9; i += 3) {
    let square = [];
    for (let j = 0; j < 3; j++) {
      const squareStyle = props.winnerList && props.winnerList.includes(i + j)
        ? { background: 'yellow' }
        : null;
      square.push(renderSquare(i + j, squareStyle));
    }
    element.push(<div class='board-row'>{ square }</div>);
  }
  return <div class='board'>{ element }</div>;
}
</script>

<style>
  .board {
    margin: 0 auto;
    width: 102px;
  }

  .board-row:after {
    clear: both;
    content: '';
    display: table;
  }
</style>
